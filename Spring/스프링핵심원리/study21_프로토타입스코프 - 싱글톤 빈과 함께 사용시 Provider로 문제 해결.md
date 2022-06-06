# :book: 스프링 핵심 원리

## :pushpin: 프로토타입 스코프

### 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 Provider로 문제 해결
- 싱글톤 빈과 프로토타입 빈을 함께 사용할 때, 어떻게 하면 사용할 때 마다 항상 새로운 프로토타입 빈을 생성할 수 있을까?

### 스프링 컨테이너에 요청
- 가장 간단한 방법은 싱글톤 빈이 프로토타입을 사용할 때마다 스프링 컨테이너에 새로 요청하는 것이다.
- 의존관계를 외부에서 주입(DI)받는게 아니라 이렇게 직접 필요한 의존관계를 찾는 것을 Dependency Lookup (DL) 의존관계
조회(탐색)이라 한다.

### ObjectFactory, ObjectProvider
- 지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스를 제공하는 것이 바로 `ObjectProvider`이다.
- 참고로 과거에는 ObjectFactory가 있었는데, 여기에 편의 기능을 추가해서 ObjectProvider가 만들어졌다.

````
@Autowired
private ObjectProvider<PrototypeBean> prototypeBeanProvider;

public int logic() {
    PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
    prototypeBean.addCount();
    int count = prototypeBean.getCount();
    return count;
}
````

- 실행해보면 `prototypeBeanProvider.getObject()`을 통해서 항상 새로운 프로토타입 빈이 생성되는 것을 확인할 수 있다.
- ObjectProvider의 getObject()를 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다. (DL)
- 스프링이 제공하는 기능을 사용하지만, 기능이 단순하므로 단위 테스트를 만들거나 mock 코드를 만들기는 훨씬 쉬어진다.
- ObjectProvider는 지금 딱 필요한 DL 정도의 기능만 제공한다.

#### 특징
- ObjectFactory: 기능이 단순, 별도의 라이브러리 필요 없음, 스프링에 의존
- ObjectProvider: ObjectFactory 상속, 옵션, 스트림 처리 등 편의 기능이 많고, 별도의 라이브러리 필요 없음, 스프링에 의존

#### 정리
- 그러면 프로토타입 빈을 언제 사용할까? 매번 사용할 때마다 의존관계 주입이 완료된 새로운 객체가 필요하면 사용하면 된다.
- 그런데 실무에서 웹 애플리케이션을 개발해보면, 싱글톤 빈으로 대부분의 문제를 해결할 수 있기에 프로토타입 빈을 직접적으로 사용하는 일은 매우 드물다.
- ObjectProvider, JSR303 Provider 등은 프로토타입 뿐만 아니라 DL이 필요한 경우는 언제든지 사용할 수 있다.

- *참고*: 스프링이 제공하는 메서드에 @Lookup 애노테이션을 사용하는 방법도 있지만, 이전 방법들로 충분하고, 고려해야할 내용도 많아서 생략하겠다.