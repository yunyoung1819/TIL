# :book: 백엔드 개발자를 위한 대용량 데이터 & 트래픽 처리
## :pushpin: Chapter 10. 데이터 정합성 보장을 위한 트랜잭션

### 1. 트랜잭션이 없는 세상
트랜잭션이 왜 필요할까요?

|이름| 잔액 |
|---|---|
|홍길동|1000|
|김국밥|500|

홍길동이 김국밥에게 900원을 송금

```text
1. READ (홍길동 잔고)
2. UPDATE (김국밥 잔액) = 김국밥 잔액 + 900
```

|이름| 잔액   |
|---|------|
|홍길동| 1000 |
|김국밥| 1400 |


```text
1. READ (홍길동 잔고)
2. UPDATE (김국밥 잔액) = 김국밥 잔액 + 900
3. UPDATE (홍길동 잔액) = 홍길동 잔액 - 900
```

|이름| 잔액  |
|---|-----|
|홍길동| 100 |
|김국밥| 1400 |

```text
1. READ (홍길동 잔고)
2. UPDATE (김국밥 잔액) = 김국밥 잔액 + 900
3. UPDATE (홍길동 잔액) = 홍길동 잔액 - 900 -> 여기서 실패한다면?
```

**여러 SQL문을 마치 하나의 오퍼레이션으로 묶을 수 있어야한다!**
>트랜잭션

![](./images/트랜잭션이없는세상.png)
**처리 중인 데이터를 다른 곳에서 조회하게 되면 문제가 발생**
> 트랜잭션 격리레벨


### 2. 트랜잭션 ACID
`ACID`(원자성, 일관성, 고립성, 지속성)는 데이터베이스 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질을 가리키는 약어.
데이터베이스에서 데이터에 대한 하나의 `논리적 실행단계`를 `트랜잭션`이라고 한다.
예를 들어 은행에서의 `계좌이체`를 트랜잭션이라고 할 수 있는데 '송신자 계좌의 금액 감소', '수신자 계좌의 금액 증가'가 한 동작으로 이루어져야 하는 것을 의미한다.

1. **원자성(Atomicity)**: 트랜잭션과 관련된 작업들이 부분적으로 실행되다가 중단되지 않는 것을 보장하는 능력
2. **일관성(Consistency)**: 트랜잭션이 실행을 성공적으로 완료하면 언제나 일관성 있는 데이터베이스 상태로 유지하는 것을 의미한다.
3. **독립성(Isolation)**: 트랜잭션을 수행 시 다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장하는 것을 의미한다. 이것은 트랜잭션 밖에 있는 어떤 연산도 중간 단계의 데이터를 볼 수 없음을 의미한다. 성능 관련 이유로 인해 이 특성은 가장 유연성 있는 제약 조건이다.
4. **지속성(Durability)**: 성공적으로 수행된 트랜잭션은 영원히 반영되어야 함을 의미한다. 시스템 문제, DB 일관성 체크 등을 하더라도 유지되어야 함을 의미한다.

<details>
<summary> ATOMICITY - 원자적 연산을 보장해야한다 </summary>
- ALL or Nothing
- 어떻게? `MVCC`를 통해

![](./images/트랜잭션동작과정1.png)
![](./images/트랜잭션동작과정2.png)
![](./images/트랜잭션동작과정3.png)
![](./images/트랜잭션동작과정4.png)
</details>

<details>
<summary>CONSISTENCY - 트랜잭션이 종료되었을 때 데이터 무결성이 보장된다</summary>
- **제약조건**을 통해 ex) 유니크 제약, 외래키 제약 등
</details>

<details>
<summary>ISOLATION - 트랜잭션은 서로 간섭하지 않고 독립적으로 동작한다</summary>
- 하지만 많은 성능을 포기해야 하므로 개발자가 제어가 가능
- 트랜잭션 격리레벨을 통해 via MVCC
</details>

<details>
<summary>DURABILITY - 완료된 트랜잭션을 유실되지 않는다</summary>
- WAL을 통해 
</details>


### 3. 트랜잭션 격리레벨
#### ISOLATION - 트랜잭션은 서로 간섭하지 않고 독립적으로 동작한다

#### 트랜잭션 격리레벨
- READ UNCOMMITTED
- READ COMMITTED
- REPEATABLE READ
- SERIALIZABLE READ

#### 3가지 이상 현상 
- Dirty Read
- Non Repeatable Read
- Phantom READ

#### Dirty Read
홍길동: 1000원
김국밥: 500원

- 홍길동이 김국밥에게 900원을 송금
- 김국밥 잔액에 대한 UPDATE가 실패했으므로 500원으로 되어야하지만 다른 트랜잭션이 업데이트가 실패하기전 잔고인 1400원을 읽어들이는 현상
- 커밋되지 않은 데이터를 읽었다고해서 `Dirty Read`라고 한다.

![](./images/더티리드1.png)
![](./images/더티리드2.png)
![](./images/더티리드3.png)
![](./images/더티리드4.png)


#### Non Repeatable Read
- 하나의 트랜잭션에서 같은 데이터를 3번 읽었는데 다른 데이터가 나오는 현상 
- 같은 데이터를 조회했는데 결과가 달라지는 것 
![](./images/nonrepetable_read1.png)
![](./images/nonrepetable_read2.png)
![](./images/nonrepetable_read3.png)
![](./images/nonrepetable_read4.png)

#### Phantom Read
- 같은 조건으로 데이터를 조회했을 때 없던 데이터가 생겼을 때 발생하는 현상

![](./images/팬텀리드1.png)
![](./images/팬텀리드2.png)
![](./images/팬텀리드3.png)


#### 트랜잭션 격리레벨
|                  | Dirty Read | Non Repetable Read | Phantom Read |
|------------------|------------|--------------------|--------------|
| Read Uncommitted | O          | O                  | O            |
|Read Committed|            | O                  | O            |
|Repetable Read| | | O |
|Serializable Read| | | |


```
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIABLE READ
```

- 아래로 갈수록 이상현상이 없음 
- 아래로 갈수록 동시 처리량이 낮다