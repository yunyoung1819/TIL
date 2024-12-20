## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

### stored function
- `사용자가 정의한 함수`
- `DBMS`에 저장되고 사용되는 `함수`
- SQL의 `select`, `insert`, `update`, `delete` statement에서 사용할 수 있다

### stored function 예제 - 1
임직원의 ID를 열자리 정수로 랜덤하게 발급하고 싶다.
ID의 맨 앞자리는 1로 고정이다.
```mysql
DROP FUNCTION IF EXISTS id_generator;

delimiter $$
create function id_generator()
returns int
no sql
begin
return (1000000000 + floor(rand() * 1000000000));
end
$$
delimiter ;
```

id_generator를 사용해서 Employee 테이블에 임직원 정보를 추가하자
```mysql
insert into employee values (id_generator(), '원희', '1991-08-04', 'F', 'PO', 1000000000, 1001);

select * from employee where name = '원희';
```

### stored function 예제 - 2
부서의 ID를 파라미터로 받으면 해당 부서의 평균 연봉을 알려주는 함수를 작성하자

```mysql
delimiter $$
create function dept_avg_salary(d_id int)
returns int
reads sql data
begin
declare avg_sal int;
select avg(salary) into avg_sal
from employee
where dept_id = d.id;
return avg_sal;
end
$$
delimiter ;

또는 

delimiter $$
create function dept_avg_salary(d_id int)
    returns int
    reads sql data
begin
    select avg(salary) into @avg_sal
    from employee
    where dept_id = d_id;
    return @avg_sal;
end
$$
delimiter ;
```

```mysql
select *, dept_avg_salary(id)
from department;
```

### stored function 예제 - 3
졸업 요건 중 하나인 토익 800 이상을 충족했는지를 알려주는 함수를 작성하자
```mysql
delimiter $$
create function toeic_pass_fail(toeic_score int)
returns char(4)
no sql
begin
declare pass_fail char(4);
if toeic_score is null then set pass_fail = 'fail';
elseif toeic_score < 800 then set pass_fail = 'fail';
else						  set pass_fail = 'pass';
end if;
return pass_fail;
end
$$
delimiter ;

delimiter $$
create function toeic_pass_fail(toeic_score int)
returns char(4)
no sql
begin
if toeic_score is null then set @pass_fail = 'fail';
elseif toeic_score < 800 then set @pass_fail = 'fail';
else						  set @pass_fail = 'pass';
end if;
return @pass_fail;
end
$$
delimiter ;
```

```mysql
select *, toeic_pass_fail(toeic)
from student;
```

### stored function
- 이외에도 loop를 돌면서 반복적인 작업을 수행하거나
- case 키워드를 사용해서 값에 따라 분기 처리하거나
- 에러를 핸들링하거나 에러를 일으키는 등의 다양한 동작을 정의할 수 있다


### sotred function 삭제하기
```mysql
DROP FUNCTION stored_function_name;
```


### 등록된 stored function 파악하기

```mysql
SHOW FUNCTION STATUS where DB = 'company';

SHOW DATABASES;

SHOW CREATE FUNCTION id_generator;
```

### stored function은 언제 써야할까?
#### Three-tier architecture

#### Presentation tier
- 사용자에게 보여지는 부분을 담당하는 tier
- HTML, javascript, CSS, native app, desktop app

#### Logic tier 
- 서비스와 관련된 기능과 정책 등등 비즈니스 로직을 담당하는 tier
- application tier, middle tier라고도 불림
- Java + Spring, Python + Django, etc...

#### Data tier
- 데이터를 저장하고 관리하고 제공하는 역할을 하는 tier
- MySQL, Oracle, SQL Server, PostgreSQL, MongoDB

#### 언제 써야 할까?
- util 함수로 쓰기에는 괜찬흥ㄹ 것 같다
- 비즈니스 로직을 stored function에 두는 것은 좋지 않을 것 같다

| stored function  | 비즈니스 로직을 가지는가? |
|------------------|----------------|
| dept_avg_salary  | X              |
| id_generator     | △              |
| toeic_pass_fail  | O              |
