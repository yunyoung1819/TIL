# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 서브쿼리

### 서브쿼리

- 나이가 평균보다 많은 회원

```
select m from Member m 
where m.age > (select avg(m2.age) from Member m2)
```