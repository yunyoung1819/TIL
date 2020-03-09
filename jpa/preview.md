
### JPA란?

- 과거에는 객체를 데이터베이스에 저장하려면 복잡한 JDBC API와 SQL을 직접 작성해야만 했다.
- JdbcTemplate이나 Mybatis가 등장해서 개발 코드는 많이 줄었지만, SQL은 직접 작성해야만 하는 문제점이 있었음
- JPA가 등장하면서 SQL조차도 직접 작성할 필요가 없어졋다.


```
public class MemberDAO {

    @PersistenceContext
    EntityManager jpa;

    public void save(Member member) {
        jpa.persist(member);
    }
    public Member findOne(Long id) {
        return jpa.find(Member.class, id);
    }
}
```

### JPA 실무에서 어려운 이유

- 처음 JPA나 스프링 데이터 JPA를 만나면?
- SQL 자동화, 수십줄의 코드가 한 두줄로!
- 실무에 바로 도입하면?
- 예제들은 보통 테이블이 한두개로 단순함
- 실무는 수십 개 이상의 복잡한 객체와 테이블 사용
