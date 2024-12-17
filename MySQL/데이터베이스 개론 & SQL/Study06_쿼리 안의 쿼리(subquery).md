## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL
### :seedling: subquery

### SELECT with subquery
ID가 14인 임직원보다 생일이 빠른 임직원의 ID, 이름, 생일을 알고 싶다
```mysql
select birth_date from employee where id = 14;

select id, name, birth_date from employee
where birth_date < '2008-02-01';
```

```mysql
select id, name, birth_date from employee
where birth_date < (
    select birth_date from employee where id = 14
);
```

- `subquery` (nested query or inner query): `SELECT`, `INSERT`, `UPDATE`, `DELETE`에 포함된 query
- outer query (main query): subquery를 포함하는 query
- subquery는 `()` 안에 기술된다


ID가 5인 임직원언과 같은 프로젝트에 참여한 임직원들의 ID를 알고 싶다
```mysql
select proj_id from works_on where empl_id = 5;

select distinct empl_id from works_on
where empl_id != 5 and proj_id in (2001, 2002);
```

```mysql
select distinct empl_id from works_on
where empl_id != 5 and proj_id in (
    select proj_id 
    from works_on 
    where empl_id = 5
);
```

### IN
- v `IN` (v1, v2, v3, ...): v가 (v1, v2, v3, ...) 중에 하나와 값이 같다면 `TRUE`를 리턴한다
- (v1, v2, v3, ...)는 명시적인 값들의 집합일 수도 있고 subquery의 결과 (set or multiset)일 수도 있다
- v `NOT IN` (v1, v2, v3, ...): v가 (v1, v2, v3, ...)의 모든 값과 값이 다르다면 `true`를 리턴한다
- unqualified attribute가 참조하는 table은 해당 attribute가 사용된 query를 포함하여 그 query의 바깥쪽으로 존재하는
모든 queries 중에 해당 attirubte 이름을 가지는 가장 가까이에 있는 table을 참조한다

### EXISTS
- `EXISTS`: subquery의 결과가 `최소 하나`의 row라도 있다면 `TRUE`를 반환
- `NOT EXISTS`: subquery의 결과가 `단 하나`의 row라도 없다면 `TRUE`를 반환

### ANY
- v comparison_operation `ANY` (subquery): subquery가 반환한 결과들 중에 단 하나라도 v와의 비교 연산이 TRUE라면 TRUE를 반환한다.
- `SOME`도 `ANY`와 같은 역할을 한다

### ALL
- v comparison_operator `ALL` (subquery): subquery가 반환한 결과들과 v와의 비교 연산이 모두 TRUE라면 TRUE를 반환한다

### 참고사항
1. 성능 비교: `IN` vs `EXISTS`
- `RDBMS`의 종류와 버전에 따라 다르며 최근 버전은 많은 개선이 이루어져서 `IN`과 `EXISTS`의 성능 차이가 거의 없는 것으로 알고 있음

2. 위 문법들은 MySQL 기준임
