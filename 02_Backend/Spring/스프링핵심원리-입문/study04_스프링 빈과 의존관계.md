# :book: 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술 (김영한)
## :pushpin: 스프링 빈과 의존관계

### 스프링 빈을 등록하고 의존관계 설정하기

- 회원 컨트롤러가 회원 서비스와 회원 리포지토리를 사용할 수 있게 의존관계를 준비하자

```java

@Controller
public class MemberController {
    
    private final MemberService memberService;
    
    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```

- 생성자에 @Autowired가 있으면 스프링이 연관된 객체를 스프링 컨테이너에서 찾아서 넣어준다. 이렇게 객체 의존 관계를 외부에서 넣어주는 것을 DI(Dependency Injection), 의존성 주입이라 한다.
- 이전 테스트에서는 개발자가 직접 주입했고, 여기서는 @Autowired에 의해 스프링이 주입해준다.

#### 스프링 빈을 등록하는 2가지 방법
1. 컴포넌트 스캔과 자동 의존관계 설정
2. 자바 코드로 직접 스프링 빈 등록하기


#### 컴포넌트 스캔과 자동 의존관계 설정
- @Component 애노테이션이 있으면 스프링 빈으로 자동 등록된다.
- @Controller 컨트롤러가 스프링 빈으로 자동 등록된 이유도 컴포넌트 스캔때문이다.
- @Component를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록된다.
  - @Controller
  - @Service
  - @Repository


참고: 생성자에 @Autowired를 사용하면 객체 생성 시점에 스프링 컨테이너에서 해당 스프링 빈을 찾아서 주입한다. 
생성자가 1개만 있으면 @Autowired는 생략할 수 있다.

참고: 스프링은 스프링 컨테이너에 스프링 빈을 등록할때 기본으로 싱글톤으로 등록한다. (유일하게 하나만 등록해서 공유한다)
따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 설정으로 싱글톤이 아니게 설정할 수 있지만, 특별한 경우를 제외하면 대부분 싱글톤을 사용한다.


### 자바 코드로 직접 스프링 빈 등록하기


```java
@Configuration
public class SpringConfig {
    
    @Bean 
    public MemberService memberService() {
        return new MemberService(memberRepository());
    }
    
    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```
- 참고: XML로 설정하는 방식도 있지만 최근에는 잘 사용하지 않으므로 생략한다.
- 참고: DI에는 필드 주입, setter 주입, 생성자 주입 이렇게 3가지 방법이 있다. 의존관계가 실행 중에 동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장한다.
- 참고: 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 컴포넌트 스캔을 사용한다. 그리고 정형화되지 않거나, 
상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다.
- 주의: @Autowired를 통한 DI는 'helloController', 'MemberService' 등과 같이 스프링이 관리하는 객체에서만 동작한다.
스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.


### 스프링 DB 접근 기술
**스프링 데이터엑세스**

H2 데이터베이스 설치
- 개발이나 테스트 용도로 가볍고 편리한 DB, 웹 화면 제공 
- https://www.h2database.com
- 다운로드 및 설치
- h2 데이터베이스 버전은 스프링부트 버전에 맞춘다.
- 권한 주기: chmod 755 h2.sh
- 실행: ./h2.sh
- 데이터베이스 파일 생성 방법
  - jdbc:h2:~/test
  - ~/test.mv.db
  - 이후부터는 jdbc:h2:tcp://localhost/~/test 이렇게 접속

개방-폐쇄 원칙(OCP, Open-Closed Principle)
- 확장에는 열려있고, 수정, 변경에는 닫혀있다.
- 스프링의 DI (Dependencies Injection)을 사용하면 기존 코드를 전혀 손대지 않고 설정만으로 구현 클래스를 변경할 수 있다.

- `@SpringBootTest`: 스프링 컨테이너와 테스트를 함께 실행한다.
- `@Transactional`: 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고 테스트 완료 후에 항상 롤백한다.
이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다.


### 스프링 JdbcTemplate
- 순수 Jdbc와 동일한 환경 설정을 하면 된다.
- 스프링 JdbcTemplate과 MyBatis 같은 라이브러리는 JDBC API에서 본 반복 코드를 대부분 제거해준다. 하지만 SQL은 직접 작성해야 한다.


### JPA
- JPA는 기존의 반복 코드는 물론이고 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
- JPA를 사용하면 SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
- JPA를 사용하면 개발 생산성을 크게 높일 수 있다.


### Spring Data JPA
- 인터페이스를 통한 기본적인 CRUD
- findByName(), findByEmail() 처럼 메서드 이름 만으로 조회 기능 제공
- 페이징 기능 자동 제공

> 참고: 실무에서는 JPA와 스프링 데이터 JPA를 기본으로 사용하고 복잡한 동적 쿼리는 Querydsl이라는 라이브러리를 사용하면 된다.
Querydsl을 사용하면 쿼리도 자바 코드도 안전하게 작성할 수 있고, 동적 쿼리도 편리하게 작성할 수 있다. 이 조합으로 해결하기 어려운 쿼리는 JPA가 제공하는 네이티브 쿼리를 ㅏ용하거나
앞서 학습한 jdbcTemplate을 사용하면 된다. 