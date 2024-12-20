## :pushpin: 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

### :seedling: ORDER BY
- 조회 결과를 **특정 attribute(s) 기준으로 정렬**하여 가져오고 싶을 때 사용한다
- `default` 정렬 방식은 `오름차순`이다
- `오름차순` 정렬은 `ASC`로 표기한다
- `내림차순` 정렬은 `DESC`로 표기한다


### :seedling: aggregate function
- 여러 tuple들의 정보를 요약해서 **하나의 값으로 추출하는 함수**
- 대표적으로 `COUNT`, `SUM`, `MAX`, `MIN`, `AVG` 함수가 있다
- (주로) 관심있는 attribute에 사용된다 e.g) AVG(salary), MAX(birth_date)
- `NULL 값들은 제외`하고 요약 값을 추출한다


### :seedling: Group By
각 프로젝트에 참여한 임직원 수와 최대 연봉과 최소 연봉과 평균 연봉을 알고 싶다
```mysql
select w.proj_id, count(*), max(salary), min(salary), avg(salary)
from works_on w 
join employee e 
on w.empl_id = e.id
group by w.proj_id;
```
- **관심있는 attribute(s) 기준으로 그룹을 나눠서 그룹별로** aggregate function을 적용하고 싶을 때 사용
- grouping attribute(s): 그룹을 나누는 기준이 되는 attribute(s)
- grouping attribute(s)에 *NULL 값이 있을 때는 NULL 값을 가지는 tuple끼리 묶인다*


### :seedling: HAVING
```mysql
select w.proj_id, count(*), max(salary), min(salary), avg(salary)
from works_on w join employee e on w.empl_id = e.id
group by w.proj_id
having count(*) >= 7;
```
- `group by`와 함께 사용한다
- aggregate function의 결과값을 바탕으로 `그룹을 필터링`하고 싶을 때 사용한다
- `having 절`에 명시된 조건을 만족하는 그룹만 `결과에 포함`된다

각 프로젝트별로 프로젝트에 참여한 90년대생들의 수와 이들의 평균 연봉을 알고 싶다

```mysql
select proj_id, count(*), round(avg(salary), 0)
from works_on w join employee e on w.empl_id = e.id
where e.birth_date between '2000-01-01' and '2010-12-31'
and w.proj_id in (select proj_id from works_on
                  group by proj_id having count(*) > 3)
group by w.proj_id
order by w.proj_id
```

### SELECT 요약
```mysql
SELECT attribute(s) or aggregate function(s)
FROM table(s)
[WHERE condition(s)]
[GROUP BY group attribute(s)]
[HAVING group condition(s)]
[ORDER BY attribute(s)];
```

### SELECT 실행순서 (개념적인 순서)
```text
6. SELECT attribute(s) or aggregate function(s)
1. FROM tables(s)
2. [WHERE condition(s)]
3. [GROUP BY group attribute(s)]
4. [HAVING group condition(s)]
5. [ORDER BY attribute(s)];
```
- select 쿼리에서 각 절(phrase)의 실행 순서는 개념적인 순서이다
- select 쿼리의 실제 실행 순서는 각 `RDBMS`에서 어떻게 구현했는지에 따라 다르다