# :book: selab-study
## :pushpin: Topic. DB 트랜잭션

### 트랜잭션(Transaction)이란?

![](../images/트랜잭션.PNG)

- 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 수행되어야할 일련의 연산들을 의미

- 하나의 작업을 수행하기 위해 필요한 데이터베이스의 연산들을 모아놓은 것

- 데이터베이스에서 논리적인 작업의 단위이며 장애가 발생했을 때 데이터를 복구하는 작업의 단위
    - 데이터베이스는 정확한 데이터를 유지 및 오류 발생 시 빠르게 복구하고, 데이터베이스가 항상 정확하고 일관된 상태를 유지할 수 있도록 
    다양한 기능을 제공하는데 가장 중요한 역할을 하는 것이 트랜잭션
    - 트랜잭션이라는 것을 관리함으로써 데이터베이스의 회복과 병행 제어가 가능

- 트랜잭션의 모든 명령문이 완벽하게 처리되거나 하나도 처리되지 않아야 데이터베이스 모순이 없는 일관된 상태를 유지

- 트랜잭션은 SELECT, UPDATE, INSERT, DELETE와 같은 연산을 수행하여 데이터베이스의 상태를 변화시키는 작업의 단위


### 트랜잭션의 특징 (ACID)

- `Atomicity (원자성)`
    - 트랜잭션이 데이터베이스에 모두 반영되던지 아니면 전혀 반영되지 않아야함.
    - 트랜잭션 내의 모든 명령은 반드시 완벽히 수행되어야 하며, 모두가 완벽히 수행되지 않고 어느 하나라도 오류가 발생하면 트랜잭션 전부가 취소되어야 함

- `Consistency (일관성)`
    - 트랜잭션의 작업 처리 결과가 항상 일관성이 있어야함
    - 시스템이 가지고 있는 고정 요소는 트랜잭션 수행 전과 수행 완료 후의 상태가 같아야함 
    
- `Isolation (독립성)`
    - 둘 이상의 트랜잭션이 동시에 실행되고 있을 경우 어떤 하나의 트랜잭션이라도 다른 트랜잭션의 연산에 끼어들 수 없다.

- `Durability (지속성)`
    - 성공적으로 완료된 트랜잭션의 결과는 시스템이 고장나더라도 영구적으로 반영되어야 함
    
    
### 트랜잭션 연산 및 상태 

#### Commit 연산
- Commit 연산은 한개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝났고 데이터베이스가 다시 일관된 상태에 있을 때
이 트랜잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산


### Rollback 연산
- Rollback 연산은 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 
정상적으로 처리되었더라도 트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산
- Rollback 시에는 해당 트랜잭션을 재시작하거나 폐기함

### 트랜잭션 상태 

![](../images/트랜잭션%20상태.PNG)

- 활동(Active): 트랜잭션이 실행 중인 상태
- 실패(Failed): 트랜잭션 실행에 오류가 발생하여 중단된 상태
- 철회(Aborted): 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
- 부분 완료(Partially Committed): 트랜잭션의 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
- 완료(Committed): 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태


### Tip. 세션과 트랜잭션 차이
- 세션
    - 어떤 활동을 위한 시간이나 기간
    - 데이터베이스 접속을 시작으로 여러 데이터베이스에서 관련 작업을 수행한 후 접속을 종료하기까지 전체 기간을 의미

- 트랜잭션과 세션의 차이
    - 트랜잭션은 DML이 모인 하나의 작업 단위를 뜻하며 세션 내부에는 하나 이상의 트랜잭션이 존재
    - 데이터베이스에 접속한 후 종료하기까지의 과정이 하나의 세션이며 이 세션이 유지되는 동안 여러 COMMIT, ROLLBACK 작업이 진행되기 때문
    - 세션이 트랜잭션보다 큰 단위
    
    
### 자주 보는 오류 메시지 
- row was updated or deleted by another transaction (or unsaved-value mapping was incorrect
    
 