## ;pushpin; 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

### SQL 뜻
- **Structured Query Language** (SQL)
- 현업에서 쓰이는 relational DBMS의 표준 언어
- 종합적인 database 언어: `DDL` + `DML` + `VDL`

### SQL 주요 용어
| relational data model  | SQL      |
|------------------------|----------|
| relation               | table    |
| attribute              | column   |
| tuple                  | row      |
| domain                 | domain   |

### SQL & RDBMS
- SQL은 RDBMS의 표준 언어이지만 실제 구현에 강제가 없기 때문에 RDBMS마다 제공하는 SQL의 스펙이 조금씩 다르다.

### DATABASE vs SCHEMA
- MySQL에서는 DATABASE와 SCHEMA가 같은 뜻을 의미
- CREATE DATABASE company = CREATE SCHEMA company
- 다른 RDBMS에서는 의미가 다르게 쓰임
- i.g PostgreSQL에서는 SCHEMA가 DATABASE의 namespace를 의

### attribute data type: 숫자
| 종류 | 설명 | 사이즈 | MySQL |
| ---------- | ---------- | ---------- | ---------- |
| 정수 | 정수를 저장할 때 사용 | 1 byte | TINYINT |
| 정수 | 정수를 저장할 때 사용 | 2 byte | SMALLINT |
| 정수 | 정수를 저장할 때 사용 | 3 byte | MEDIUMINT |
| 정수 | 정수를 저장할 때 사용 | 4 byte | INT or INTEGER |
| 정수 | 정수를 저장할 때 사용 | 8 byte | BIGINT |
| 부동 소수점 방식 | 실수를 저장할 때 사용. 고정소수점 방식에 비해 정확하지 않다 | 4 byte | FLOAT|
| 부동 소수점 방식 | 실수를 저장할 때 사용. 고정소수점 방식에 비해 정확하지 않다 | 8 byte | DOUBLE or DOUBLE PRECISION |
| 고정 소수점 방식 | 실수를 정확하게 저장할 때 사용 | variable | DECIMAL or NUMERIC |

### attribute data type: 문자열
| 종류 | 설명                                                                                   | MySQL |
| --- |--------------------------------------------------------------------------------------| --- |
| 고정크기 문자열 | 최대 몇 개의 '문자'를 가지는 문자열을 저장할지를 지정. 저장될 문자열의 길이가 최대 길이보다 작으면 나머지를 space로 채워서 저장 ('a  ') | CHAR(n) |
| 가변크기 문자열 | 최대 몇 개의 '문자'를 가지는 문자열을 저장할지를 지정. 저장될 문자열의 길이 만큼만 저장 ('a')                            | VARCHAR(n) |
| 사이즈가 큰 문자열 | 사이즈가 큰 문자열을 저장할 때 사용                                                                 | TINYTEXT, TEXT, MEDIUMTEXT, LONGTEXT | 

### attribute data type: 날짜와 시간
| 종류 | 설명                                                                  | MySQL                |
| --- |---------------------------------------------------------------------|----------------------|
| 날짜 | 년,월,일을 저장 (YYYY-MM-DD)                                              | DATE                 |
| 시간 | 시,분,초를 저장 (hh:mm:ss or hhh:mm:ss                                    | TIME                 |
| 날짜와 시간 | 날짜와 시간을 같이 표현. (YYYY-MM-DD hh:mm:ss) TIMESTAMP는 time-zone이 반영됨      | DATETIME, TIMESTAMP  |

### attribute data type: 그 외
| 종류 | 설명 | MySQL |
| --- | --- | --- |
| byte-string | (문자열이 아니라) byte string을 저장 | BINARY, VARBINARY, BLOB type |
| boolean | true, false를 저장. MySQL에는 따로 없음 | TINYINT로 대체 사용 |
| 위치 관련 | 위치 관련 정보를 저장 | GEOMETRY etc |
| JSON | json 형태의 데이터를 저장 {"name": "messi", "age":38} | JSON |

### Key constraints: PRIMARY KEY
- primary key: table의 `tuple`을 식별하기 위해 사용, 하나 이상의 `attribute(s)`로 구성
- primary key는 중복된 값을 가질 수 없으며, NULL도 값으로 가질 수 없다.
- primary key를 선언하는 방법

attribute 하나로 구성될 때
```mysql
create table PLAYER(
    id INT PRIMARY KEY 
);
```
attribute 하나 이상으로 구성될 때
```mysql
create table PLAYER(
    team_id VARCHAR(12),
    back_number INT,
    PRIMARY KEY (team_id, back_number)
);

```
### key constraints: UNIQUE
- UNIQUE로 지정된 attribute(s)는 중복된 값을 가질 수 없다
- 단 NULL은 중복을 허용할 수도 있다 (RDBMS마다 다름)

attribute 하나로 구성될 때
```mysql
create table PLAYER(
    id INT UNIQUE
);
```

attribute 하나 이상으로 구성될 때 
```mysql
create table PLAYER(
    team_id VARCHAR(12),
    back_number INT,
    UNIQUE(team_id, back_number)
);
```

### attribute DEFAULT
- 새로운 tuple을 저장할 때 해당 attribute에 대한 값이 없다면 default 값으로 저장
```sql
create table Orders (
  menu varchar(15) default '짜장면',   
);
```

### CHECK constraint
- attribute의 값을 제한하고 싶을 떄 사용
```mysql
create table EMPLOYEE(
    age INT CHECK (age >= 36)
);
```
```mysql
create table PROJECT(
    start_date DATE,
    end_date DATE,
    CHECK (start_date < PROJECT.end_date)
);
```

### FOREGIN KEY
- attribute가 다른 table의 primary key나 unique key를 참조할 때 사용 
```mysql
create table Employee(
    dept_id INT,
    FOREIGN KEY (dept_Id)
                     references DEPARTMENT(id)
                     on delete reference_option
                     on update reference_option
)
```

### constraint 이름 명시하기
- 이름을 붙이면 어떤 constraint를 위반했는지 쉽게 파악할 수 있음
- constraint를 삭제하고 싶을 때 해당 이름으로 삭제 가능
```mysql
create table TEST(
  age INT CONSTRAINT age_over_20 CHECK (oge> 20)  
);
```

### ALTER TABLE
- table의 schema를 변경하고 싶을 때 사용
- 이미 서비스 중인 talbe의 schema를 변경하는 것이라면 변경 작업 때문에 서비스의 백엔드에 영향이 없을지 검토한 후에 변경하는 것이 중요

| 유형 | MySQL 예제                                               |
| --- |--------------------------------------------------------|
| attribute 추가 | alter table employee add blood varchar(2);             |
| attribute 이름 변경 | alter table employee rename column phone to phone_num; |
| attribute 타입 변경 | alter table employee modify column blood char(2);      
| table 이름 변경 | alter table logs rename to backend_logs;               |
| primary key 추가 | alter table log add priamry key (id); |

### DROP TABLE
- table을 삭제할 때 사용
- DROP TABLE table_name;

