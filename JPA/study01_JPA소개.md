## JPA와 모던 자바 데이터 저장 기술

### SQL 중심적인 개발의 문제점
- 애플리케이션 객체 지향 언어 - Java, Scala, ...
- 데이터베이스 세계의 헤게모니 관계형 DB - Oracle, MySQL, ...
- 지금 시대는 객체를 관계형 DB에 관리 - SQL! SQL!! SQL!!!
- SQL에 의존적인 개발을 피하기 어렵다.
- 무한 반복, 지루한 코드
- 계층형 아키텍처 => 진정한 의미의 계층 분할이 어렵다.
- 객체답게 모델링 할수록 매핑 작업만 늘어난다.
- 객체를 자바 컬렉션에 저장하듯이 DB에 저장할 수는 없을까? => JPA (Java Persistence API)


### 패러다임의 불일치
- 객체 vs 관계형 데이터베이스
>객체 지향 프로그래밍은 *추상화, *캡슐화, *정보은닉, *상속, *다형성 등 시스템의 복잡성을 제어할 수 있는
다양한 장치들을 제공한다.

- 객체를 영구 보관하는 다양한 저장소 (Object -> RDB, NoSQL, File 등)
- 현실적인 대안은 관계형 데이터베이스


### 객체와 관계형 데이터베이스의 차이
- 상속
- 연관관계
- 데이터 타입
- 데이터 식별 방법

### 객체 그래프 탐색
- 객체는 자유롭게 객체 그래프를 탐색할 수 있어야한다.
- 처음 실행하는 SQL 범위에 따라 탐색 범위 결정

```
SELECT M.*, T.*
FROM MEMBER M
JOIN TEAM T ON M.TEAM_ID = T.TEAM_ID

member.getTeam();   // OK
member.getOrder();  // null
```
