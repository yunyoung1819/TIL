# pushpin: 토비의 스프링6
## :seedling: 템플릿

### 스프링과 JDK 업그레이드

### 템플릿 (Template)
#### 개방 폐쇄 원칙 (OCP)
- 클래스나 모듈은 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다
- 변화의 특성이 다른 부분을 구분하고 각각 다른 목적과 이유에 의해 다른 시점에 독립적으로 변경될 수 있는 효율적인 구조를 만들어야 한다

![](./images/017.png)

#### 템플릿
> 코드 중에서 변경이 거의 일어나지 않으며 일정한 패턴으로 유지되는 특성을 가진 부분을 
> 자유롭게 변경되는 성질을 가진 부분으로부터 독립시켜서 효과적으로 활용할 수 있도록 하는 방법

- 변경이 거의 일어나지 않ㅇ며 일정한 패턴으로 유지되는 특성을 가진 부분: 템플릿
- 자유롭게 변경되는 성질을 가진 부분: 콜백


#### WebApiExRateProvider 리팩토링 

#### 변하는 코드 분리하기 (메소드 추출)
WebApiExRateProvider의 구성
1. URI를 준비하고 예외처리를 위한 작업을 하는 코드
2. API를 실행하고 서버로부터 받은 응답을 가져오는 코드
3. JSON 문자열을 파싱하고 필요한 환율 정보를 추출하는 코드

```java
public BigDecimal getExRate(String currency) {
    String url = "http://open.er-api.com/v6/latest/" + currency;
    
    URI uri;
    try {
        uri = new URI(url);
    } catch (URISyntaxException e) {
        throw new RuntimeException(e);
    }
    
    String response;
    try {
        HttpURLConnection connection = (HttpURLConnection) uri.toURL().openConnection();
        try (BufferedReader br = new BufferedReader(new InputStreamReader(connection.getInputStream()))) {
            reponse = br.lines().collect(Collectors.joining());
        } 
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
    
    try {
        ObjectMapper mapper = new ObjectMapper();
        ExRateData data = mapper.raedValue(response, ExRateData.class);
        return data.rates().get("KRW");
    } catch (JsonProcessingException e) {
        throw new RuntimeException(e);
    }
}
```

- 일단 메소드 추출로 분리해봅시다

```java
public class WebApiExRateProvider implements ExRateProvider {

    @Override
    public BigDecimal getExRate(String currency) {
        String url = "https://open.er-api.com/v6/latest/" + currency;

        URI uri;
        try {
            uri = new URI(url);
        } catch (URISyntaxException e) {
            throw new RuntimeException(e);
        }

        String response;
        try {
            response = executeApi(uri);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }

        try {
            return parseExRate(response);
        } catch (JsonProcessingException e) {
            throw new RuntimeException(e);
        }
    }

    private static BigDecimal parseExRate(String response) throws JsonProcessingException {
        ObjectMapper mapper = new ObjectMapper();
        ExRateData data = mapper.readValue(response, ExRateData.class);
        return data.rates().get("KRW");
    }

    private static String executeApi(URI uri) throws IOException {
        String response;
        HttpURLConnection connection = (HttpURLConnection) uri.toURL().openConnection();
        try (BufferedReader br = new BufferedReader(new InputStreamReader(connection.getInputStream()))) {
            response = br.lines().collect(Collectors.joining());
        }
        return response;
    }
}
```


#### 변하지 않는 코드 분리하기 (메소드 추출 - 템플릿의 탄생)
**템플릿(Template)**: 템플릿은 어떤 목적을 위해 미리 만들어둔 모양이 있는 틀. 
고정된 틀 안에 바꿀 수 있는 부분을 넣어서 사용하도록 만들어진 오브젝트.
템플릿 메소드 패턴도 템플릿을 사용


#### 템플릿 메소드 패턴?
템플릿 메소드 패턴은 고정된 틀의 로직을 가진 템플릿 메소드를 슈퍼클래스에 두고, 바뀌는 부분을 서브클래스의 메소드에 두는 구조로 이뤄진다

#### 지금 만들고 있는 템플릿에 적용되는 디자인 패턴은?
- 일단 메소드 추출로 분리해봅시다

#### ApiExecutor 분리
- 인터페이스 도입과 클래스 분리

#### ApiExecutor 콜백과 메소드 주입
**콜백(Callback)**
- 콜백은 실행되는 것을 목적으로 다른 오브젝트의 메소드에 전달되는 오브젝트
- 파라미터로 전달되지만 값을 참조하기 위한 것이 아니라 특정 로직을 담은 메소드를 실행시키는 것이 목적
- 하나의 메소드를 가진 인터페이스 타입(SAM)의 오브젝트 또는 람다 오브젝트

#### 템플릿/콜백은 전략 패턴의 특별한 케이스
- 템플릿은 전략 패턴의 컨텍스트
- 콜백은 전략 패턴의 전략
- 템플릿/콜백은 메소드 하나만 가진 전략 인터페이스를 사용하는 전략 패턴


#### 메소드 주입
- 의존 오브젝트가 메소드 호출 시점에 파라미터로 전달되는 방식
- 의존관계 주입의 한 종류
- 메소드 호출 주입(method call injection)이라고도 한다.


#### ApiTemplate 분리
- 환율정보 API로부터 환율을 가져오는 기능을 제공하는 오브젝트
- API 호출과 정보 추출의 기본 틀 제공
- 두 가지 콜백을 이용
- 유사한 여러 오브젝트에서 재사용 가능


#### 스프링이 제공하는 템플릿
> RestTemplate, JdbcTemplate, JmsTemplate, TransactionTemplate, JpaTemplate, HibernateTemplate...

RestTemplate: HTTP API 요청을 처리하는 템플릿
- HTTP Client 라이브러리 확장: ClientHttpRequestFactory
- Message Body를 변환하는 전략: HttpMessageConverter

ClientHttpRequestFactory: HTTP Client 기술을 사용해서 ClientHttpRequest를 생성하는 전략
- SimpleClientHttpRequest (HttpURLConnection)
- JdkClientHttpRequest (HttpClient)
- NettyClientRequest (HttpClient)
- NettyClientRequest
- JettyClientRequest
- OkHttp3ClientRequest

doExecute(): HTTP API 호출 workflow를 가지고 있는 템플릿 메소드로 두 개의 콜백을 받음
- RequestCallback
  - void doWithRequest(ClientHttpRequest request) throws IOException;
- ResponseExtractor
  - T extractData(ClientHttpResponse response) throws IOException;
- execute(), getForObject(), postForEntity(), ... 등등의 편리한 메소드 제공 


#### 스프링의 템플릿
- JdbcTemplate
- JmsTemplate
- TransactionTemplate
- HibernateTemplate
- ~~JpaTemplate~~

MyBatis
- SqlSessionTemplate


#### 템플릿/콜백 패턴
- 템플릿/콜백 패턴에서 템플릿은 여러 상황에서 반복되는 고정된 실행 절차나 구조를 의미합니다. 변하는 부분은 콜백 객체에 위임하여 템플릿 자체는 수정없이 재사용됩니다.
- 콜백은 템플릿이 제공하는 고정된 구조 안에서 필요에 따라 다르게 실행되어야 하는 가변적인 로직을 담은 객체입니다. 템플릿은 정해진 흐름에 따라 콜백의 메소드를 호출합니다.


#### Quiz
1. 객체 지향 설계의 5대 원칙(SOLID) 중 OCP(개방/폐쇄 원칙)의 핵심 내용은 무엇인가요?
>OCP는 새로운 기능을 추가할 때 기존 코드를 수정하지 않고 확장을 통해 추가할 수 있도록 설계해야 함을 의미합니다.
> 이를 통해 시스템의 변화에 유연하게 대처할 수 있게 됩니다. 

2. 템플릿/콜백 패턴에서 템플릿이 나타내는 코드 부분은 무엇인가요?
> 템플릿/콜백 패턴에서 템플릿은 여러 상황에서 반복되는 고정된 실행 절차나 구조를 의미합니다. 변하는 부분은 콜백 객체에 위임하여 템플릿 자체는 수정없이 재사용됩니다.

3. 템플릿/콜백 패턴에서 콜백이 나타내는 코드 부분은 무엇인가요?
> 콜백은 템플릿이 제공하는 고정된 구조 안에서 필요에 따라 다르게 실행되어야 하는 가변적인 로직을 담은 객체입니다. 템플릿은 정해진 흐름에 따라 콜백의 메소드를 호출합니다.

4. 네트워크 통신 중 발생할 수 있는 Checked Exception을 RuntimeException으로 감싸서 처리한 주된 이유는 무엇일까요?
> 네트워크 오류처럼 호출하는 곳에서 특별히 복구할 방법이 없는 예외는 Runtime Exception으로 처리하여 호출 코드를 간결하게 유지할 수 있습니다. Checked Exception은 호출자에게 반드시 처리를 강제합니다.

5. 자바에서 `InputStream`이나 `BufferedReader`와 같이 사용 후 반드시 해제해야하는 리소스를 안전하게 관리하는 가장 권장되는 방법은 무엇인가요?
> `try-with-resources`는 AutoCloseable 인터페이스를 구현한 객체를 try 선언부에 사용하면 블록이 끝날 때 정상 종료되거나 예외 발생 여부에 상관없이 리소스가 자동으로 안전하게 해제됩니다.

6. 템플릿/콜백 패턴은 변하는 부분을 인터페이스로 분리하고 템플릿이 해당 인터페이스를 사용하도록 함으로써 OCP를 만족시킵니다. 이는 어떤 디자인 패턴과 유사한 구조인가요?
> 전략 패턴에서 컨텍스트(Context)는 템플릿에 해당하고 전략(Strategy)은 콜백에 해당합니다. 변하지 않는 컨텍스트가 변하는 전략 객체를 필요에 따라 바꿔가며 사용합니다.

8. 템플릿 객체를 스프링 빈으로 등록하여 여러 곳에서 공유(싱글톤)하기 위해 템플릿 클래스 설계 시 가장 중요하게 고려해야할 점은 무엇인가요?
> 싱글톤 빈은 여러 스레드에서 동시에 접근할 수 있으므로, 내부 상태가 변경 가능하면 스레드 안전성 문제가 발생할 수 있습니다. 불변(Immutable) 객체이거나 스레드 안전하게 설계되어야 싱글톤으로 사용하기에 적합합니다. 

9. 템플릿/콜백 패턴 구조에서 클라이언트(Client)의 주요 역할은 무엇인가요?
> 클라이언트는 특정 작업을 수행하기 위해 템플릿을 사용하며, 이때 템플릿의 가변적인 부분에 해당하는 콜백 객체를 직접 생성하거나 다른 곳에서 가져와 템플릿 메소드를 호출하며 전달하는 역할을 합니다.

10. 스프링이 제공하는 다양한 템플릿 객체들 중 HTTP 기반의 REST API 호출을 편리하게 수행하도록 돕는 것은 무엇인가요?
> RestTemplate은 스프링에서 제공하는 HTTP 클라이언트로 RESTful 서비스 호출 시 복잡한 연결 및 응답 처리 과정을 템플릿-콜백 패턴을 활용하여 간소화해줍니다. 