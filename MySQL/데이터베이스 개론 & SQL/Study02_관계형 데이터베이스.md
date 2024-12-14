## ;pushpin; 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

## relational data model
### set
- 서로 다른 `elements`를 가지는 `colleciton`
- 하나의 `set`에서 `element`의 순서는 중요하지 않다.
  - e.g. `{1,3,11,4,7}`

### student relation in relational data model
**STUDENT**

| id | name | grade | major | phone_num | emer_phone_num |
| --- | --- | --- | --- | --- | --- |
| 2022022 | 윤영 | 4 | 컴퓨터 | 010-1234-5678 | 010-3456-1234 |
| 2022023 | 이주미 | 4 | 사회복지학과 | 010-3333-4444 | 010-9999-9999 |
| 2022024 | 김예은 | 4 | 컴퓨터 | 010-1234-6666 | 010-7777-8888 |

![](../images/relation.png)
- `attribute`: id, name, grade, major, phone_num, emer_phone_num
- `tuple`: 2022022 윤영 4 컴퓨터 010-1234-5678 010-3456-1234

### relation data model
- `domain`: set of atomic value
- `domain name`: domain 이름
- `attribute`: domain이 relation에서 맡은 역할 이름
- `tuple`: 각 attribute의 값으로 이루어진 리스트. 일부 값은 NULL일 수 있다.
- `relation`: set of tuples
- `relation name`: relation 의 이름 

### relation schema
- `relation`의 구조를 나타낸다
- `relation 이름`과 `attributes 리스트`로 표기된다
- e.g STUDENT(id, name, grade, major, phone_num, emer_phone_num)
- attributes 와 관련된 `constraints`도 포함한다.

### degree of a relation
- relation schema에서 attributes의 수 (e.g 6)

### relational database
- **relational data model에 기반하여 구조화된 database**
- `relational database`는 여러 개의 `relations`로 구성된다.

### relation의 특징들
1. **`relation`은 중복된 `tuple`을 가질 수 없다**(relation is set of tuples) set은 중복을 허용하지 않음 
2. **`relation`의 `tuple을 식별`하기 위해 `attribute의 부분 집합`을 `key`로 설정한다**
3. **`relation`에서 `tuple`의 순서는 중요하지 않다**
4. **하나의 `relation`에서 `attribute`의 이름은 중복되면 안된다**
5. **하나의 `tuple`에서 attribute의 순서는 중요하지 않다**
6. **`attribute`는 `atmoic` 해야 한다 (composite or multivalued attribute 허용 안됨)**

### NULL의 의미
1. 값이 존재하지 않는다
2. 값이 존재하나 아직 그 값이 무엇인지 알지 못한다
3. 해당 사항과 관련이 없다

## Key
### super key
- relation에서 tuples를 **unique**하게 식별할 수 있는 attributes set
- e.g. PLAYER(id, name, team_id, back_number, birth_date)의 super key는
{id, name, team_id, back_number, birth_date}, {id, name}, {name, team_id, back_number}, ... etc

### candidate key
- 어느 한 attribute라도 제거하면 unique하게 tuples를 식별할 수 없는 super key
- key or minimal superkey
- e.g. PLAYER(id, name, team_id, back_number, birth_date)의 candidate key는
{id}, {team_id, back_number}

### primary key
- relation에서 tuples를 **unique**하게 식별하기 위해 선택된 candidate key
-  e.g. PLAYER(id, name, team_id, back_number, birth_date)의 primary key는
{id} or {team_id, back_number}

### unique key
= primary key가 아닌 candidate keys
- alternate key
- e.g. PLAYER(id, name, team_id, back_number, birth_date)의 unique key는
{team_id, back_number}

### foreign key
- 다른 relation의 PK를 참조하는 attribute set
- e.g. PLAYER(id, name, team_id, back_number, birth_date)와 TEAM(id, name, manager)가 있을 때
foreign key는 PLAYER의 {team_id}

### constraints
- relational database의 relations들이 언제나 항상 지켜줘야 하는 제약 사항
  - `domain constraints`: attribute의 value는 해당 attribute의 도메인에 속한 value여야 한다.
  - `key constraints`: 서로 다른 tuples는 같은 value의 key를 가질 수 없다.
  - `NULL value constraints`: attribute가 NOT NULL로 명시됐다면 NULL을 값으로 가질 수 없다.
  - `entity integrity constraint`: primary key는 value에 NULL을 가질 수 없다.
  - `referential integrity constraint`: FK와 PK와 도메인이 같아야 하고 PK에 없는 values를 FK가 값으로 가질 수 없다.