## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL
### SELECT statement
- ID가 9인 임직원의 이름과 직군을 알고 싶다
```mysql
SELECT name, position FROM employee WHERE id = 9;
```

```mysql
SELECT attribute(s)
FROM table(s)
[WHERE condition(s)];
```

### AS 사용하기
- AS는 테이블이나 attribute에 `별칭(alias)`을 붙일 때 사용한다
- AS는 생략 가능하다

### DISTINCT 사용하기
- `DISTINCT`는 select 결과에서 중복되는 tuples은 제외하고 싶을 때 사용한다

```mysql
select distinct p.id, p.name
from employee as e, works_on as w, project as p
where e.position = 'DSGN'
and e.id = w.empl_id and w.proj_id = p.id;
```

### LIKE 사용하기
이름이 N으로 시작하거나 N으로 끝나는 임직원들의 이름을 알고 싶다

```mysql
select name
from employee
where name like 'N%' or name like '%N';
```

이름에 NG가 들어가는 임직원들의 이름을 알고 싶다
```mysql
select name
from employee
where name like '%NG%';
```

이름이 J로 시작하는 총 네글자의 이름을 가지는 임직원들의 이름을 알고 싶다
```mysql
select name from employee where name like 'J___';
```

## escape 문자와 함께 LIKE 사용하기
%로 시작하거나 _로 끝나는 프로젝트 이름을 찾고 싶다면?

```mysql
select name from project where name like '\%%' or name like '%\_';
```
### LIKE 정리
- `LIKE`: 문자열 pattern matching에 사용
- `%` 0개 이상의 임의의 개수를 가지는 문자들을 의미
- `_` 하나의 문자를 의미
- `\` 예약 문자를 escape 시켜서 문자 본연의 문자로 사용하고 싶을 때 사용

### * (asterik) 사용하기 
- `*`(asterik)는 선택된 tuples의 모든 attributes를 보여주고 싶을 때 사용한다

### SELECT without WHERE
- 테이블에 있는 모든 tuples를 반환한다

### 주의사항
1. `SELECT`로 조회할 때 조건들을 포함해서 조회를 한다면 이 조건들과 관련된 attributes에 index가 걸려있어야 한다.
그렇지 않다면 데이터가 많아질수록 조회 속도가 느려진다.

i.g) SELECT * FROM employee WHERE position = 'dev_back';