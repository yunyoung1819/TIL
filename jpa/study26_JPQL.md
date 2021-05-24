# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: JPQL

### JPQL 소개

- JPQL은 객체지향 쿼리 언어다. 따라서 테이블을 대상으로 쿼리하는 것이 아니라 엔티티 객체를 대상으로 쿼리한다.
- **JPQL은 SQL을 추상화해서 특정 데이터베이스 SQL에 의존하지 않는다.**
- JPQL은 결국 SQL로 변환된다.

![](./image/jpql1.png)


### JPQL 문법 1

```
select_문::=
    select_절
    from_절
    [where_절]
    [groupby_절]
    [having_절]
    [orderby_절]
    
update_문 ::= update_절 [where_절]
delete_문 :: = delete_절 [where_절]
```


### JPQL 문법 2

- select m from Member as m where m.age > 18
- 엔티티와 속성은 대소문자 구분 O (Member, age)
- JPQL 키워드는 대소문자 구분 X (SELECT, FROM, where)
- 엔티티 이름 사용, 테이블 이름이 아님 (Member)
- 별칭은 필수 (m) (as는 생략 가능)