# :book: selab-study
## :pushpin: Topic. Spring과 Spring Boot 차이

### Spring Framework

> 스프링 프레임워크는 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 간단히 스프링이라고 불린다.
> 동적인 웹 사이트를 개발하기 위한 여러가지 서비스를 제공하고 있다.

#### 장점
- `경량 컨테이너`
- `IoC` (Inversion of Control: 제어 역행)
- `DI` (Dependency Injection: 의존성 주입)
- `AOP` (Aspect-Oriented Programming: 관점지향 프로그래밍)

### Spring Boot
> 스프링 프레임워크는 기능이 많은만큼 환경 설정이 복잡한 편이다. 
> 이에 어려움을 느끼는 사용자들을 위해 나온 것이 바로 스프링 부트다.
> 스프링 부트는 스프링 프레임워크를 사용하기 위한 설정의 많은 부분을 자동화하여 
> 편리하게 스프링을 활용할 수 있도록 돕는다.


### Spring과 Spring Boot의 차이점
1.`Embeded Tomcat`을 사용하기 때문에 따로 Tomcat을 설치하거나 매번 버전을 관리해주어야 하는 수고로움을 덜어줌
2. `starter`를 통한 `dependency 자동화`
   - 과거 spring framework에서는 각각의 dependency들이 호환되는 버전을 일일이 맞추어 주어야 했디.
   - 따라서 하나의 버전을 올리고자 하면 다른 dependency에 까지 영향을 미쳐 버전 관리에 어려움이 많았다.
   - starter가 대부분의 dependency를 관리해 주기 때문에 이러한 걱정을 많이 덜게 되었다.
3. `XML` 설정을 하지 않아도 됨
4. `jar file`을 이용해 자바 옵션만으로 손쉽게 `배포` 가능