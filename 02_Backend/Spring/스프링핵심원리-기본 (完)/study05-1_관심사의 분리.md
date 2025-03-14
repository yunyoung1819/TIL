# :book: 스프링 핵심 원리

## :pushpin: 관심사의 분리

- 애플리케이션을 하나의 공연이라 생각해보자. 각각의 인터페이스를 배역(배우 역할)이라 생각하자.
그런데! 실제 배역 맞는 배우를 선택하는 것은 누가 하는가?
  
- 로미오와 줄리엣 공연을 하면 로미오 역할을 누가 할지 줄리엣 역할을 누가 할지는 배우들이 정하는게 아니다.
이전 코드는 마치 로미오 역할(인터페이스)을 하는 레오나르도 디카프리오(구현체, 배우)가 줄리엣 역할(인터페이스)을
  하는 여자 주인공 (구현체, 배우)을 직접 초빙하는 것과 같다. 디카프리오는 공연도 해야하고 동시에 여자 주인공도
  공연에 직접 초빙해야 하는 **다양한 책임**을 가지고 있다.
  
### 관심사를 분리하자
- 배우는 본인의 역할인 배역을 수행하는 것에만 집중해야 한다.
- 디카프리오는 어떤 여자 주인공이 선택되더라도 똑같이 공연을 할 수 있어야 한다.
- 공연을 구성하고, 담당 배우를 섭외하고, 역할에 맞는 배우를 지정하는 책임을 담당하는 별도의 **공연 기획자**가
나올 시점이다.
  
- 공연 기획자를 만들고, 배우와 공연 기획자의 책임을 확실히 분리하자.

### AppConfig의 등장
- 애플리케이션의 전체 동작 방식을 구성(config)하기 위해, **구현 객체를 생성**하고, **연결**하는 책임을 가지는
별도의 설정 클래스를 만들자.
  

```
public class AppConfig {

    public MemberService memberService() {
        return new MemberServiceImpl(new MemoryMemberRepository());
    }
    
    public OrderService orderService() {
        return new OrderServiceImpl(new MemoryMemberRepository(), new FixDiscountPolicy());
    }
}
```

- AppConfig는 애플리케이션의 실제 동작에 필요한 구현 객체를 생성한다.
  - MemberServiceImpl
  - MemoryMemberRepository
  - OrderServiceImpl
  - FixDiscountPolicy
  
- AppConfig는 생성한 객체 인스턴스의 참조(레퍼런)를 생성자를 통해서 주입(연결)해준다.
  - MemberServiceImp --> MemoryMemberRepository
  - OrderServiceImpl --> MemoryMemberRepository, FixDiscountPolicy
  

```
package hello.core.member;

public class MemberServiceImpl implements MemberService {

    private final MemberRepository memberRepository;

    public MemberServiceImpl(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Override
    public void join(Member member) {
        memberRepository.save(member);
    }

    @Override
    public Member findMember(Long memberId) {
        return memberRepository.findById(memberId);
    }
}
```

- 설계 변경으로 `MemberServiceImpl`은 `MemoryMemberRepository`를 의존하지 않는다.
- 단지 `MemberRepository` 인터페이스에만 의존한다.
- MemberServiceImpl 입장에서 생성자를 통해 어떤 구현 객체가 들어올지(주입될지)는 알 수 없다.
- MemberServiceImpl의 생성자를 통해서 어떤 구현 객체를 주입할지는 오직 외부(AppConfig)에서 결정된다.
- MemberServiceImpl은 이제부터 의존관계에 대한 고민은 외부에 맡기고 실행에만 집중하면 된다.

![](image/AppConfig분리.png)

- 객체의 생성과 연결은 `AppConfig`가 담당한다.
  - DIP 완성: MemberServiceImpl은 MemberRepository인 추상에만 의존하면 된다. 이제 구체 클래스를 몰라도 된다.
- 관심사의 분리: 객체를 생성하고 연결하는 역할과 실행하는 역할이 명확히 분리되었다.

- appConfig 객체는 memoryMemberRepository 객체를 생성하고 그 참조값을 memberServiceImpl을 생성하면서
생성자로 전달한다.
  
- 클라이언트인 `memberSrivceImpl` 입장에서 보면 의존관계를 마치 외부에서 주입해주는 것 같다고 해서
`DI(Dependency Injection)` 우리말로 의존관계 주입 또는 의존성 주입이라고 한다.
  

```
public class OrderServiceTest {

    MemberService memberService;
    OrderService orderService;

    @BeforeEach
    public void beforeEach() {
        AppConfig appConfig = new AppConfig();
        memberService = appConfig.memberService();
        orderService = appConfig.orderService();
    }

    @Test
    void createOrder() {
        Long memberId = 1L;
        Member member = new Member(memberId, "손나은", Grade.VIP);
        memberService.join(member);

        Order order = orderService.createOrder(memberId, "아이맥", 10000);
        Assertions.assertThat(order.getDiscountPrice()).isEqualTo(1000);
    }
}
```

- `@BeforeEach` : 테스트 코드에서 `@BeforeEach`는 각 테스트를 실행하기 전에 호출된다.
- AppConfig를 통해서 관심사를 확실하게 분리했다.
- 배역, 배우를 생각해보자.
- AppConfig는 공연 기획자다.
- AppConfig는 구체 클래스를 선택한다. 배역에 맞는 담당 배우를 선택한다. 애플리케이션이 어떻게 동작해야 할지 전체 구성을 책임진다.
- 이제 각 배우들은 담당 기능을 실행하는 책임만 지면 된다.
- OrderServiceImpl은 기능을 실행하는 책임만 지면 된다. 


### 새로운 구조와 할인 정책 적용
- 처음으로 돌아가서 정액 할인 정책을 정률 % 할인 정책으로 변경해보자.
- FixDiscountPolicy -> RateDiscountPolicy
- 어떤 부분만 변경하면 되겠는가?
  - `AppConfig`에서 할인 정책 역할을 담당하는 구현을 FixDiscountPolicy -> RateDiscountPolicy 객체로 변경했다.
  - 이제 할인 정책을 변경해도, 애플리케이션의 구성 역할을 담당하는 AppConfig만 변경하면 된다. 클라이언트 코드인
  OrderServiceImpl를 포함해서 사용 영역의 어떤 코드도 변경할 필요가 없다.
  - 구성 영역은 당연히 변경된다. 구성 역할을 담당하는 AppConfig를 애플리케이션이라는 공연의 기획자로 생각하자.
  공연 기획자는 공연 참여자인 구현 객체들을 모두 알아야 한다.

> AppConfig의 등장으로 애플리케이션이 크게 사용 영역과, 객체를 생성하고 구성(Configuration)하는 영역으로 분리되었다.

- 사용, 구성의 분리
![](image/AppConfig1.png)
  
- 할인 정책의 변경
![](image/AppConfig2.png)
  

### 전체 흐름 정리
- 새로운 할인 정책 개발
- 새로운 할인 정책 적용과 문제점
  - 새로 개발한 정률 할인 정책을 적용하려고 하니 클라이언트 코드인 주문 서비스 구현체도 함께 변경해야함
  - 주문 서비스 클라이언트가 인터페이스인 DiscountPolicy뿐만 아니라, 구체 클래스인 FixDiscountPolicy도 함께 의존 -> DIP 위반
- 관심사의 분리
- AppConfig 리팩터링
- 새로운 구조와 할인 정책 적요 
  

### 좋은 객체 지향 설계의 5가지 원칙의 적용
- 여기서 3가지 SRP, DIP, OCP 적용

> SRP 단일 책임 원칙 "한 클래스는 하나의 책임만 가져야 한다. "

> DIP 의존관계 역전 원칙 "프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다. 의존성 주입은 이 원칙을 따르는 방법 중 하나다."

> OCP "소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다"