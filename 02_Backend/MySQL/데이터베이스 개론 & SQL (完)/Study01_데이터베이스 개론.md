## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

### database (DB)
- 전자적으로 (electronically) 저장되고 사용되는 관련있는(related) 데이터들의 
조직화된 집합(organized collection)


### DBMS 
- database management systems
- 사용자에게 DB를 정의하고 만들고 관리하는 기능을 제공하는 소프트웨어 시스템
  - DB를 정의하다보면 부가적인 데이터가 발생한다


### metadata
- database를 정의하거나 기술하는(describe) data
- catalog라고도 부름
- e.g.) 데이터 유형, 구조, 제약 조건, 보안, 저장, 인덱스, 사용자 그룹 등등
- metadata 또한 DBMS를 통해 저장/관리된다


### database system
- database + DBMS + 연관된 applications
- 줄여서 database 라고도 부름


### data models
- DB의 구조(structure)를 기술하는데 사용될 수 있는 개념들이 모인 집합
- DB 구조를 `추상화`해서 표현할 수 있는 수단을 제공한다
- data model은 여러 종류가 있으며 추상화 수준과 DB 구조화 방식이 조금씩 다르다
- DB에서 읽고 쓰기 위한 기본적인 동작들(operations)도 포함한다


### data models 분류
- conceptual (or high-level) data models
- logical (or representational) data models
- physical (or low-level) data models


### conceptual data models
- 일반 사용자들이 쉽게 이해할 수 있는 개념들로 이루어진 모델
- 추상화 수준이 가장 높음
- 비즈니스 요구 사항을 추상화하여 기술할 때 사용
- entity-relationship model (ER diagram)


### logical data models
- 이해하기 어렵지 않으면서도 디테일하게 DB를 구조화할 수 있는 개념들을 제공
- 데이터가 컴퓨터에 저장될 떄의 구조와 크게 다르지 않게 DB 구조화를 가능하게 함
- 특정 DBMS나 storage에 종속되지 않는 수준에서 DB를 구조화할 수 있는 모델
- relational data model

student

| student id | 이름 | 전공 | 학년 |
|---| --- | --- | --- |
|sid_2022022 | 김연아 | 피겨 | 1 |
|sid_2022023 | 손흥민 | 축구 | 2 |
|sid_2022032 | 최민정 | 쇼트트랙 | 2 |


### logical data models 종류
- relational data model
- object data model
- object-relational data model


### physical data models
- 컴퓨터에 데이터가 어떻게 파일 형태로 저장되는지를 기술할 수 있는 수단을 제공
- data format, data orderings, access path 등등
- access path: 데이터 검색을 빠르게 하기 위한 구조체, e.g.) index


### database schema
- data model을 바탕으로 database의 구조를 기술한 것
- schema는 database를 설계할 때 정해지며 한번 정해진 후에는 자주 바뀌지 않는다


### database state
- database에 있는 실제 데이터는 꽤 자주 바뀔 수 있다
- 특정 시점에 database에 있는 데이터를 database state 혹은 snapshot 이라고 한다
- 혹은 database에 있는 현재 instances의 집합이라고도 한다


### three-schema architecture
- external schemas
- conceptual schemas
- internal schemas


### database language
- data definition language (DDL)
- storage definition language (SDL)
- view definition language (VDL)

### data manipulation language (DML)
- database에 있는 data를 활용하기 위한 언어
- data 추가, 삭제, 수정, 검색 등등의 기능을 제공하는 언어

### 통합된 언어
- 오늘날의 DBMS는 DML, VDL, DDL이 따로 존재하기보다는 통합된 언어로 존재
- 대표적인 예가 relational database language: SQL