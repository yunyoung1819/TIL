## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

### stored procedure
- 사용자가 정의한 프로시저
- RDBMS에 저장되고 사용되는 프로시저
- 구체적인 하나의 태스크(task)를 수행한다

### 두 정수의 곱셈 결과를 가져오는 프로시저를 작성하자
```mysql
delimiter $$
create procedure product(in a int, in b int, out result int)
begin
    set result = a * b;
end
$$
delimiter ;

call product(3, 5, @result);
select @result;
```


### 두 정수를 맞바꾸는 프로시저를 작성하자 (swap)
```mysql
delimiter $$
create procedure swap(inout a int, inout b int)
begin
set @temp = a;
set a = b;
set b = @temp;
end
$$
delimiter ;

set @a = 5, @b = 7;
call swap(@a, @b);
select @a, @b;
```

### 각 부서별 평균 연봉을 가져오는 프로시저를 작성하자
```mysql
delimiter $$
create procedure get_dept_avg_salary()
begin 
    select dept_id, avg(salary)
    from employee
    group by dept_id;
end $$
delimiter ;

call get_dept_avg_salary()
```

### 사용자가 프로필 닉네임을 바꾸면 이전 닉네임을 로그에 저장하고 새 닉네임으로 업데이트하는 프로시저를 작성하자
```mysql
delimiter $$
create procedure change_nickname(user_id int, new_nick varchar(30))
begin 
    insert into nickname_logs(
                             select id, nickname, now() from users where id = user_id
        );
    update users set nickname = new_nick where id = user_id;
end 
$$
delimiter ;

call change_nickname(1, 'ZIDANE');

select * from users;
select * from nickname_logs;
```

### stored procedure
- 이외에도 조건문을 통해 분기처리를 하거나
- 반복문을 수행하거나
- 에러를 핸들링하거나 에러를 일으키는 등의 다양한 로직을 정의할 수 있다

### stored procedure vs stored function

|            | stored procedure      | stored function     |
|------------|-----------------------|---------------------|
| create 문법  | create procedure ...  | create function ... |
| return 키워드로 값 반환 | 불가능 | 가능 |
| 파라미터로 값(들) 반환 | 가능 | 일부 가능 |
| 값을 꼭 반환해야 하나? | 필수 아님 | 필수 |
| SQL statement에서 호출 | 불가능 | 가능 |
| transaction 사용 | 가능 | 대부분 불가능 |
| 주된 사용 목적 | business loginc | computation |

### PROCEDURE
- `return` 키워드로 값 반환 불가능
- 파라미티로 값(들) 반환 가능

```mysql
delimiter $$
create procedure product(in a int, in b int, out result int)
begin 
    set result = a * b
end $$
delimiter ;
```

```mysql
delimiter $$
create procedure change_nickname(user_id int, new_nick varchar(30))
begin 
    insert into nickname_logs (
        select id, nickname, now() from users where id = user_id
    );
    update users set nickname = new_nickname where id = user_id;
end $$
delimiter ;
```
- 반드시 무언가를 반환할 필요 없음

### FUNCTION
- return 키워드로 값 반환 가능
- 파라미터로 값(들) 반환 불가능 

```mysql
delimiter $$
create function product(a int, b int)
returns int
no sql
begin 
    return a * b;
end $$
delimiter ;
```

```mysql
select *, product(price, order_count) from orders;
```
- product가 stored function이라면 SQL statement에서 호출 가능


