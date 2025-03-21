# :book: 자바 ORM 프로그래밍 기본편 

## :pushpin: 일대다[1:N]


### 일대다 단방향

![일대다](image/일대다단방향.png)


### 일대다 단방향 정리

- 일대다 단방향은 일대다(1:N)에서 일(1)이 연관관계의 주인
- 테이블 일대다 관계는 항상 다(N) 쪽에 외래 키가 있음
- 객체와 테이블의 차이 때문에 반대편 테이블의 외래 키를 관리하는 특이한 구조
- @JoinColumn을 꼭 사용해야 함. 그렇지 않으면 조인 테이블 방식을 사용함 (중간에 테이블을 하나 추가함)


### 일대다 단방향 정리

- 일대다 단방향 매핑의 단점
    - 엔티티가 관리하는 외래 키가 다른 테이블에 있음
    - 연관관계 관리를 위해 추가로 UPDATE SQL 실행
- 일대다 단방향 매핑보다는 다대일 양방향 매핑을 사용하자


### 일대다 양방향

![일대다](image/일대다양방향.png)


### 일대다 양방향 정리

- 이런 매핑은 공식적으로 존재 X
- @JoinColumn(insertable=false, updatable=false)
- 읽기 전용 필드를 사용해서 양방향 처럼 사용하는 방법
- 다대일 양방향을 사용하자 

