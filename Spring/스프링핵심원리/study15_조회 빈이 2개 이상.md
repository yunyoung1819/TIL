# :book: 스프링 핵심 원리

## :pushpin: 조회 빈이 2개 이상 - 문제


### 조회 빈이 2개 이상 - 문제

- `@Autowired`는 타입(Type)으로 조회한다.

```
@Autowired
private DiscountPolicy discountPolicy
```

- 타입으로 조회하기 때문에, 마치 다음 코드와 유사하게 동작한다. (실제로는 더 많은 기능을 제공한다)
- ac.getBean(DiscountPolicy.class)
- 스프링 빈 조회에서 학습했듯이 타입으로 조회하면 선택된 빈이 2개 이상일 때 문제가 발생한다.
- DiscountPolicy의 하위 타입인 FixDiscountPolicy, RateDiscountPolicy 둘 다 스프링 빈으로 선언해보자.

```
@Component
public class FixDiscountPolicy implements DiscountPolicy {}
```

```
@Component
public class RateDiscountPolicy implements DiscountPolicy {}
```

- 그리고 이렇게 의존관계 자동 주입을 실행하면 

```
@Autowired
private DiscountPolicy discountPolicy
```

- NoUniqueBeanDefinitionException 오류가 발생한다.
- 오류 메시지가 친절하게도 하나의 빈을 기대했는데 fixDiscountPolicy, rateDiscountPolicy 2개가 발견되었다고 알려준다.
- 이때 하위 타입으로 지정할 수도 있지만, 하위 타입으로 지정하는 것은 DIP를 위배하고 유연성이 떨어진다.
- 그리고 이름만 다르고, 완전히 똑같은 타입의 스프링 빈이 2개 있을 때 해결이 안된다.
- 스프링 빈을 수동 등록해서 문제를 해결해도 되지만, 의존 관계 자동 주입에서 해결하는 여러 방법이 있다.


### @Autowired 필드 명, @Quilifier, @Primary

- 해결 방법을 하나씩 알아보자.
- 조회 대상 빈이 2개 이상일 때 해결 방법
    - @Autowired 필드 명 매칭
    - @Quilifier -> @Quilifier끼리 매칭 -> 빈 이름 매칭
    - @Primary 사용

  
### @Autowired 필드 명 매칭
- @Autowired는 타입 매칭을 시도하고, 이때 여러 빈이 있으면 필드 이름, 파라미터 이름으로 빈 이름을 추가 매칭한다.

```
@Autowired
private DiscountPolicy discountPolicy
```

- 필드 명을 빈 이름으로 변경
````
@Autowired
private DiscountPolicy rateDiscountPolicy
````

- 필드 명이 'rateDiscountPolicy' 이므로 정상 주입된다.
- **필드 명 매칭은 먼저 타입 매칭을 시도하고 그 결과에 여러 빈이 있을 때 추가로 동작하는 기능**이다.


### @Autowired 매칭 정리
1. 타입 매칭
2. 타입 매칭의 결과가 2개 이상일 때 필드 명, 파라미터 명으로 빈 이름 매칭


### @Quilifier 사용
- `@Quilifier`는 추가 구분자를 붙여주는 방법이다. 주입 시 추가적인 방법을 제공하는 것이지 빈 이름을 변경하는 것은 아니다.
- 빈 등록시 @Quilifier를 붙여준다.

```
@Component
@Qualifier("mainDiscountPolicy")
public class RateDiscountPolicy implements DiscountPolicy {}
```

```
@Component
@Qualifier("fixDiscountPolicy")
public class FixDiscountPolicy implements DiscountPolicy {}
```

- **주입 시에 @Qualifier를 붙여주고 등록한 이름을 적어준다.**

- 생성자 자동 주입 예시
````
@Autowired
public OrderServiceImpl(MemberRepository memberRepository, 
                        @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) 
{
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
````

`````
@Autowired
public DiscountPolicy setDiscountPolicy(@Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
    return discountPolicy;
}
`````

- @Qualifier로 주입할 때 @Qualifier("mainDiscountPolicy")를 못찾으면 어떻게 될까?
- 그러면 mainDiscountPolicy라는 이름의 스프링 빈을 추가로 찾는다.
- 하지만 경험상 @Qualifier는 @Qualifier를 찾는 용도로만 사용하는게 명확하고 좋다.
  
- 다음과 같이 직접 빈 등록 시에도 @Qualifier를 동일하게 사용할 수 있다.

```
@Bean
@Qualifier("mainDiscountPolicy")
public DiscountPolicy discountPolicy() {
    return new ...
}
```

### Qualifier 정리
1. @Qualifier 끼리 매칭
2. 빈 이름 매칭
3. NoSuchBeanDefinitionException 발생


### @Primary 사용
- `@Primary`는 우선순위를 정하는 방법이다. @Autowired 시에 여러번 매칭되면 @Primary가 우선권을 가진다.
- rateDiscountPolicy가 우선권을 가지도록 하자

```
@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy {}

@Component
public class FixDiscountPolicy implements DiscountPolicy {}
```

- 여기까지 보면 @Primary와 @Qualifier 중에 어떤 것을 사용하면 좋을지 고민이 될 것이다.
- @Qualifier의 단점은 주입 받을 때 다음과 같이 모든 코드에 @Qualifier를 붙여주어야 한다는 점이다.

```text
@Autowired
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
```

- 반면에 @Primary를 사용하면 이렇게 @Qualifier를 붙일 필요가 없다.


### @Primary, @Qualifier 활용
- 코드에서 자주 사용하는 메인 데이터베이스의 커넥션을 획득하는 스프링 빈이 있고, 코드에서 특별한 기능으로 가끔 사용하는
서브 데이터베이스의 커넥션을 획득하는 스프링 빈이 있다고 생각해보자.
- 메인 데이터베이스의 커넥션을 획득하는 스프링 빈은 @Primary를 적용해서 조회하는 곳에서 @Qualifier 지정 없이 편리하게 조회하고,
서브 데이터베이스 커넥션 빈을 획득할 때는 @Qualifier를 지정해서 명시적으로 획득하는 방식으로 사용하면 코드를 깔끔하게 유지할 수 있다.
- 물론 이때 메인 데이터베이스의 스프링 빈을 등록할 때 @Qualifier를 지정해주는 것은 상관없다.


### 우선순위
- @Primary는 기본값 처럼 동작하는 것이고, @Qualifier는 매우 상세하게 동작한다.
- 이련 경우 어떤 것이 우선권을 가져갈까?
- 스프링은 자동보다는 수동이, 넓은 범위의 선택권보다는 좁은 범위의 선택권이 우선 순위가 높다.
- 따라서 여기서도 @Qualifier가 우선권이 높다.