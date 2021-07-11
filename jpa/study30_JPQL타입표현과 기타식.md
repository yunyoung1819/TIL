# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: JPQL 타입 표현

### JPQL 타입 표현

- 문자: 'HELLO', 'She"s'
- 숫자: 10L(Long), 10D(Double), 10F(Float)
- Boolean: TRUE, FALSE
- ENUM: jpabook.MemberType.Admin (패키지명 포함)
- 엔티티 타입: TYPE(m) = Member (상속관계에서 사용)
````
em.createQuery("select i from Item i where type(i) = Book", Item.class)
    .getResultList();
````

### JPQL 기타

- SQL과 문법이 같은 식
- EXISTS, IN
- AND, OR, NOT
- =, >, >=, <, <=, <>
- BETWEEN, LIKE, IS NULL