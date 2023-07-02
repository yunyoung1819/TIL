# :book: 백엔드 개발자를 위한 대용량 데이터 & 트래픽 처리
## :pushpin: Chapter 11. 동시성 제어하기
### :seedling: 멀티 스레드 환경에 대한 이해

### 동시성
- 대부분 하나의 웹 서버는 여러 개의 요청을 동시에 수행할 수 있다.
- 작성한 코드 한 줄은 동시에 수행될 수 있다.
- 하나의 자원을 두고 여러 개의 연산들이 경합 -> 데이터 정합성을 깨뜨릴 수 있다.

- 100원을 출금하는 요청이 동시에 발생한다면
![](./images/출금요청.png)
![](./images/동시성.png)

### 데이터베이스에서 동시성 이슈가 발생하는 일반적인 패턴
1. 공유자원 조회 

-> 다른 오퍼레이션 수행

2. 공유자원 갱신

### 공유 자원에 대한 잠금을 획득하여 줄 세우기
![](./images/동시성이슈1.png)
![](./images/동시성이슈2.png)

### 동시성 이슈가 어려운 이유
1. 로컬에서는 대부분 하나의 스레드로 테스트
2. 이슈가 발생하더라도 오류가 발생하지 않는다
3. 코드에서 잘 보이지 않는다.
4. 항상 발생하지 않고 비결정적으로 발생한다

### 작성한 코드 한 줄은 동시에 수행될 수 있다

### :seedling: 쓰기락과 읽기락
- 동시성 제어를 위한 가장 보편적인 방법은 락을 통한 줄세우기

![](./images/동시성제어락.png)

- 락을 통해 `동시성`을 제어할 때는 **락의 범위를 최소화**하는 것이 중요
- MySQL에서는 트랜잭션의 `커밋` 혹은 `롤백`시점에 잠금이 풀린다.
  - **트랜잭션이 곧 락의 범위**
- **MySQL**에서는 `쓰기락`, `읽기락` 두 가지 잠금을 제공

| | 읽기락(Shared Lock) | 쓰기락(Exclusive Lock) |
|---|---|---|
| 읽기락(Shared Lock) | O | 대기 |
| 쓰기락(Exclusive Lock) | 대기 | 대기 |

- 읽기락은 SELECT ... FOR SHARE
- 쓰기락은 SELECT ... FOR UPDATE 또는 UPDATE, DELETE 쿼리
- 매번 잠금이 발생할 경우 성능저하를 피할 수 없음
  - MySQL에서 일반 SELECT는 nonblocking consistent read로 동작
  - https://dev.mysql.com/doc/refman/5.7/en/innodb-consistent-read.html
- MySQL에서 잠금은 row가 아니라 인덱스를 잠근다
  - 인덱스가 없는 조건으로 Locking Read시 불필요한 데이터들이 잠길 수 있음

### 락 확인하기
```text
// 락 상태 확인
select * from performance_schema.data_locks
```

````
// 트랜잭션 상태 확인
select * from information_schema.innodb_trx;
````

### 추가로 공부해볼만한 것들
- Java에서의 동시성 이슈 제어 방법
- 분산환경에서의 동시성 이슈 제어방법
- MySQL의 넥스트 키락이 등장한 배경
- MySQL 외래키로 인한 잠금
- MySQL 데드락