# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 서브쿼리

### 서브쿼리

- 나이가 평균보다 많은 회원

```
select m from Member m 
where m.age > (select avg(m2.age) from Member m2)
```

- 한 건이라도 주문한 고객
```
select m from Member m
where (select count(o) from Order o where m = o.member) > 0
```


### 서브 쿼리 지원 함수

- [NOT] EXISTS (subquery): 서브쿼리에 결과가 존재하면 참
- {ALL | ANY | SOME} (subquery)
- ALL 모두 만족하면 참
- ANY, SOME: 같은 의미, 조건을 하나라도 만족하면 참

- [NOT] IN (subquery) : 서브쿼리의 결과 중 하나라도 같은 것이 있으면 참 


### 서브쿼리 예제

- 팀 A 소속인 회원
- select m from Member m
where exists (select t from m.team t where t.name = '팀A')
  
- 전체 상품 각각의 재고보다 주문량이 많은 주문들
- select o from Order o
where o.orderAmount > ALL (select p.stockAmount from Product p)
  
- 어떤 팀이든 팀에 소속된 회원
- select m from Member m
where m.team = ANY (select t from Team t)
  

### JPA 서브 쿼리 한계

- JPA는 WHERE, HAVING 절에서만 서브 쿼리 사용 가능
- SELECT 절도 가능 (하이버네이트에서 지원)
- **FROM 절의 서브 쿼리는 현재 JPQL에서 불가능**
    - 조인으로 풀 수 있으면 풀어서 해결
    