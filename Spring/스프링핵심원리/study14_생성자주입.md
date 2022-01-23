# :book: 스프링 핵심 원리

## :pushpin: 생성자 주입

### 생성자 주입을 선택해라!

> 과거에는 수정자 주입과 필드 주입을 많이 사용했지만, 최근에는 스프링을 포함한 DI 프레임워크 대부분이 생성자 주입을 권장한다.
> 그 이유는 다음과 같다.

#### **불변**

- 대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 오히려 대부분의 의존관계는
애플리케이션 종료 전까지 변하면 안된다. (불변해야 한다.)
- 수정자 주입을 사용하면, setXxx 메서드를 public으로 열어두어야 한다.
- 누군가 실수로 변경할 수도 있고, 변경하면 안되는 메서드를 열어두는 것은 좋은 설계 방법이 아니다.
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없다. 따라서 불변하게 설계할 수 있다.

#### **누락**

- 프레임워크 없이 순수한 자바 코드를 단위 테스트하는 경우에
- 다음과 같이 수정자 의존관계인 경우

```java
public class OrderServiceImpl implements OrderService {
    
    private MemberRepository memberRepository;
    private DiscountPolicy discountPolicy;
    
    @Autowired
    public void setMemberRepository(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
    
    @Autowired
    public void setDiscountPolicy(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }
}
```

- @Autowired가 프레임워크 안에서 동작할 때는 의존관계가 없으면 오류가 발생하지만, 지금은 프레임워크 없이 순수한 
자바 코드로만 단위 테스트를 수행하고 있다.
- 이렇게 테스트를 수행하면 실행은 된다.
```
@Test
void createOrder() {
    OrderServiceImpl orderService = new OrderServiceImpl();
    orderService.craateOrder(1L, "itemA", 10000);    
}
```

- 그런데 막상 실행 결과는 NPE(Null Point Exception)이 발생하는데, memberRepository, discountPolicy 모두 
의존관계 주입이 누락되었기 때문이다.
- 생성자 주입을 사용하면 다음처럼 주입 데이터를 누락했을 때 컴파일 오류가 발생한다.
- 그리고 IDE에서 바로 어떤 값을 필수로 주입해야 하는지 알 수 있다.

#### ** final 키워드**

- 생성자 주입을 사용하면 필드에 `final` 키워드를 사용할 수 있다. 그래서 생성자에서 혹시라도 값이 설정되지 않는 오류를
컴파일 시점에 막아준다. 다음 코드를 보자.
  
```java
@Component
public class OrderServiceImpl implements OrderService {
    
    private final MemberRepository memberRepository;
    private final DiscountPolicy discountPolicy;
    
    @Autowired
    public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
    }
}
```
- 잘보면 필수 필드인 discountPolicy에 값을 설정해야 하는데, 이 부분이 누락되었다. 자바는 컴파일 시점에 다음 오류를 발생시킨다.class 
- java: variable discountPolicy might not have been initialized
- 기억하자! **컴파일 오류는 세상에서 가장 빠르고, 좋은 오류다!**

> 참고: 수정자 주입을 포함한 나머지 주입 방식은 모두 생성자 이후에 호출되므로 필드에 final 키워드를 사용할 수 없다.
> 오직 생성자 주입 방식만 final 키워드를 사용할 수 있다.

#### 정리
- 생성자 주입 방식을 선택하는 이유는 여러가지가 있지만, 프레임워크에 의존하지 않고, 순수한 자바 언어의 특징을 잘 살리는 방법이기도 하다.
- 기본으로 생성자 주입을 사용하고, 필수 값이 아닌 경우에는 수정자 주입 방식을 옵션으로 부여하면 된다. 
- 생성자 주입과 수정자 주입을 동시에 사용할 수 있다.
- **항상 생성자 주입을 선택해라! 그리고 가끔 옵션이 필요하면 수정자 주입을 선택해라. 필드 주입은 사용하지 않는게 좋다.**


### 롬복과 최신 트렌드
- 막상 개발을 해보면, 대부분이 다 불변이고 그래서 다음과 같이 생성자에 final 키워드를 사용하게 된다.
- 그런데 생성자도 만들어야 하고, 주입받은 값을 대입하는 코드도 만들어야 하고...
- 필드 주입처럼 좀 편리하게 사용하는 방법은 없을까?
- 다음 기본 코드를 최적화해보자.

```java
@Component
public class OrderServiceImpl implements OrderService {
    
    private final MemberRepository memberRepository;
    private final DiscountPolicy discountPolicy;
    
    @Autowired
    public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = discountPolicy;
    }
}
```

- 생성자가 딱 1개만 있으면 @Autowired를 생략할 수 있다.

- 이제 롬복을 적용해보자. 
- 롬복 라이브러리가 제공하는 `@RequiredArgsConstructor` 기능을 사용하면 final 이 붙은 필드를 모아서 생성자를
자동으로 만들어준다. (다음 코드에는 보이지 않지만 실제 호출 가능하다)
- 최종 결과는 다음과 같다! 정말 간결하지 않은가!

````java
@Component
@RequiredArgsConstructor
public class OrderServiceImpl implements OrderService {
    
    private final MemberRepository memberRepository;
    private final DiscountPolicy discountPolicy;
}
````

- 이 최종결과 코드와 이전의 코드는 완전히 동일하다.
- 롬복이 자바의 애노테이션 프로세서라는 기능을 이용해서 컴파일 시점에 생성자 코드를 자동으로 생성해준다.
- 실제 class를 열어보면 다음 코드가 추가되어 있는 것을 확인할 수 있다.

```
public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
```

### 정리 
- 최근에는 생성자를 딱 1개 두고 `@Autowired`를 생략하는 방법을 주로 사용한다. 
- 여기에 Lombok 라이브러리의 `@RequiredArgsConstructor` 함께 사용하면 기능은 다 제공하면서, 코드는 깔끔하게 사용할 수 있다.