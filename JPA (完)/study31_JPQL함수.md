# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: JPQL 함수

### JPQL 기본 함수
- CONCAT
- SUBSTRING
- TRIM
- LOWER, UPPER
- LENGTH
- LOCATE
- ABS, SQRT, MOD
- SIZE, INDEX(JPA 용도)

### 사용자 정의 함수 호출
- 하이버네이트는 사용전 방언에 추가해야 한다.
    - 사용하는 DB 방언을 상속받고, 사용자 정의 함수를 등록한다.
```
select function('group_concat', i.name) from Item i
```
  
- 사용자 정의 함수 등록
```
public class MyH2Dialect extends H2Dialect {
  
  public MyH2Dialect() {
    registerFunction("group_concat", new StandardSQLFunction("group_concat", standardBasicTypes.STRING));
  }
}
```

- persistence.xml
```
<properties>
    <property name="hibernate.dialect" value="dialect.MyH2Dialect" />
</properties>
```

- JpaMain.java
```
String query = "select function('group_concat', m.username) From Member m";
```

- 하이버네이트에서는 아래와 같이 사용할 수도 있다.
```
String query = "select group_concat(m.username) From Member m";
```