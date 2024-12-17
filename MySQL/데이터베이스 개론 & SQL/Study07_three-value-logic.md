## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL
### :seedling: SQL에서 NULL의 의미
- `unknown`
- `unavailable` or `withheld`
- `not applicable`

```mysql
select id from employee where birth_date = null;  (X)

select id from employee where birth_date is null;  (O)
```

### NULL과 SQL three-value logic
- `SQL`에서 `NULL`과 비교 연산을 하게 되면 그 결과는 `UNKNOWN` 이다
- unknown은 **'true일수도 있고 false일 수도 있다'** 라는 의미이다
- `three-valued logic`: 비교/논리 연산의 결과로 `true`, `false`, `unknown`을 가진다

| 비교 연산 예제    | 결과     |
|-------------|--------|
| 1 = 1       | true   |
| 1 != 1      | false |
| 1 = NULL    | unknown |
| 1 != NULL   | unknown |
| 1 > NULL    | unknown |
| 1 <= NULL   | unknown |
| NULL = NULL | unknown |


### WHERE 절의 condition(s)
- where 절에 있는 condition(s)의 결과가 `true`인 `tuple(s)`만 선택된다
- 즉, 결과가 `false`거나 `unknown`이면 **tuple은 선택되지 않는다**

### NOT IN 사용시 주의 사항
`v NOT IN(v1, v2, v3)`는 아래와 같은 의미이다

> v != v1 AND v != v2 AND v != v3 <br>
> 만약 v1, v2, v3 중에 하나가 NULL 이라면?

| NOT IN 예제             | 결과 |
|-----------------------| --- | 
| 3 not in (1, 2, 4)    | true |
| 3 not in (1, 2, 3)    | false |
| 3 not in (1, 3, NULL) | false |
| 3 not in (1, 2, NULL) | unknown |

```mysql
select d.id, d.name
from department as d 
where d.id not in (
        select e.dept_id
        from employee e 
        where e.birth_date >= '2000-01-01'
    );
```

birth_date에 `null`이 있다면 condition는 unknown이 된다.
즉 의도한 결과가 나오지 않는다. 따라서 아래 쿼리처럼 `is not null` 또는 `exists`로 수정해야한다.

```mysql
select d.id, d.name
from department as d
where d.id not in (
    select e.dept_id
    from employee e
    where e.birth_date >= '2000-01-01'
      and e.dept_id is not null
);
```
또는
```mysql
select d.id, d.name
from department as d 
where not exists (
    select * 
    from employee e 
    where e.dept_id = d.id and e.birth_date >= '2000-01-01'
);
```


