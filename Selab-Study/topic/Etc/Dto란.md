# :book: selab-study
## :pushpin: Topic. Entity, DAO, DTO


### DAO(Data Access Object)란?

- 실제로 DB에 접근하는 객체
- `Persistence` Layer(DB에 data를 CRUD하는 계층)
- Service와 DB를 연결하는 고리 역할
- SQL을 사용하여 DB에 접근한 후 적절한 CRUD API를 제공함
- JPA의 경우 기본적인 CRUD 메서드를 제공함

```java
public interface UserRepository extends UserRepository<User, Long> {
    
}
```

### Entity
- 실제 `DB 테이블`과 매핑되는 클래스
- 데이터베이스의 테이블에 존재하는 `컬럼`들을 필드로 가지는 객체
- @Entity, @Column, @Id 등을 이용

```java
@Entity
public class Post {
    private String title;
    private String content;
    private String author;
}
```


### Dto
- Data Transfer Object의 약자
- `계층 간 데이터 교환`을 위한 객체(Java Beans)
- DTO는 계층간 데이터 교환이 이루어질 수 있도록 하는 객체이기 때문에 특별한 로직을 가지지 않는 **순수한 데이터 객체**이어야 한다.

```java
@Getter
public class UserDto {
    @NotBlank
    private String email;
    
    private String password;
    
    private String name;
}
```


### VO(Value Object) vs Dto

- VO는 DTO와 동일한 개념이지만 read only 속성을 가진다.
- `VO`는 특정한 비즈니스 값을 담는 객체이고, `DTO`는 Layer 간의 통신 용도로 오고가는 객체


### Entity와 Dto를 분리하는 이유
- View Layer와 DB Layer의 역할을 철저하게 분리하기 위해서
- 테이블과 매핑되는 Entity 클래스가 변경되면 여러 클래스에 영향을 끼치게 되는 
반면 View와 통신하는 DTO 클래스(Request/Response)는 자주 변경되므로 분리해야 한다.
- DTO는 Domain Model을 복사한 형태로 다양한 Presentation Logic을 추가한 정도로 사용하며
Domain Model 객체는 Persistent 만을 위해서 사용함
