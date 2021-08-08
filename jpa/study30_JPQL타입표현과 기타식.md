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


### 조건식 - CASE 식

- 기본 CASE 식

````
select 
    case when m.age <= 10 then '학생요금'
         when m.age >= 60 then '경로요금'
         else '일반요금'
    end
from Member m
````

- 단순 CASE 식

```
select
    case t.name
        when '팀A' then '인센티브110%'
        when '팀B' then '인센티브120%'
        else '인센티브105%'
    end
from Team t
```

- COALESCE: 하나씩 조회해서 null이 아니면 반환
- NULLIF: 두 값이 같으면 null 반환, 다르면 첫번째 값 반환

- 사용자 이름이 없으면 이름 없는 회원을 반환

````
select coalesce(m.username, '이름 없는 회원') from Member m
````

- 사용자 이름이 '관리자'면 null을 반환하고 나머지는 본인의 이름을 반환

````
select NULLIF (m.username, '관리자') from Member m
````