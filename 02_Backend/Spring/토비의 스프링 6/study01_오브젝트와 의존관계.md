## pushpin: 토비의 스프링6

### 오브젝트와 의존관계
- 오브젝트 (Object): 겍체

### 클래스와 오브젝트
- 클래스는 오브젝트를 만드는 청사진이다.
- 클래스의 인스턴스(Class Instance) = 오브젝트
- 자바에서는 배열(Array)도 오브젝트
- 위 두가지가 자바에서 오브젝트이다.

### 의존관계 Dependency
- A ---> B
- A가 B에 의존한다.

![](./images/001.png)

- Client의 기능이 제대로 동작하려면 Supplier가 필요
- Client가 Supplier를 사용, 호출, 생성, 인스턴스화, 전송
- 클래스 레벨(코드 레벨)의 의존관계: Supplier가 변경되면 Client 코드가 영향을 받는다.

### 관심사의 분리 (Separation of Concerns, SoC)