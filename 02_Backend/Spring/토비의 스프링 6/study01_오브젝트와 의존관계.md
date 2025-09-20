## pushpin: 토비의 스프링6

#### 오브젝트와 의존관계
- 오브젝트 (Object): OOP, 객체, 클래스?

#### 클래스와 오브젝트
- 클래스의 인스턴스(Class Instance) = 오브젝트
- 자바에서는 배열(Array)도 오브젝트
- 위 두가지가 자바에서 오브젝트이다.

#### 의존관계 Dependency
- A ---> B
- A가 B에 의존한다.

![](./images/001.png)

- Client의 기능이 제대로 동작하려면 Supplier가 필요
- Client가 Supplier를 사용, 호출, 생성, 인스턴스화, 전송
- 클래스 레벨(코드 레벨)의 의존관계: Supplier가 변경되면 Client 코드가 영향을 받는다.

#### 관심사의 분리 (Separation of Concerns, SoC)
- 관심사: Separation of Concerns (SoC)
- 관심사 분리 전
  - PaymentService
    - prepare()

- 관심사 분리 후
  - PaymentService
    - prepare()
    - getExRate()

![](./images/002.png)

#### 상속을 통한 확장

![](./images/003.png)

#### 클래스의 분리

![](./images/004.png)

#### 인터페이스 도입

![](./images/005.png)

#### 관계설정 책임의 분리

![](./images/006.png)

