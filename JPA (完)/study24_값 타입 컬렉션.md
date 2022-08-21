# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 값 타입 컬렉션

### 값 타입 컬렉션

![값타입컬렉션](./image/값타입컬렉션.PNG)

```a
@Entity
public class Member {

    @Id
    @GeneratedValue
    @Column(name = "MEMBER_ID")
    private Long id;
    
    @Column(name = "USERNAME")
    private String username;
    
    @Embedded
    private Address homeAddress;
    
    @ElementCollection
    @CollectionTable(name = "FAVORITE_FOOD", joinColumns =
        @JoinColumn(name = "MEMBER_ID")
    )
    @Column(name = "FOOD_NAME")
    private Set<String> favoriteFoods = new HashSet<>();
    
    @ElementCollection
    @CollectionTable(name = "ADDRESS", joinColumns =
        @JoinColumn(name = "MEMBER_ID")
    )
    private List<Address> addressHistory = new ArrayList<>();
    
}
```

### 값 타입 컬렉션

- 값 타입을 하나 이상 저장할 때 사용
- @ElementCollection, @CollectionTable 사용
- 데이터베이스는 컬렉션을 같은 테이블에 저장할 수 없다.
- 컬렉션을 저장하기 위한 별도의 테이블이 필요함

### 값 타입 컬렉션 사용
- 값 타입 저장 예제
```
public class JpaMain {

    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");
        EntityManager em = emf.createEntityManager();
        
        EntityTransaction tx = em.getTransaction();
        tx.begin();
        
        try {    
        
            Member member = new Member();
            member.setUsername("member1");
            member.setHomeAddress(new Address("homeCity", "street", "10000"));
            
            member.getFavoriteFoods().add("비빔밥");
            member.getFavoriteFoods().add("치킨");
            member.getFavoriteFoods().add("삼겹살");
            
            member.getAddressHistory().add(new Address("old1", "street", "10000"));
            member.getAddressHistory().add(new Address("old2", "street", "10000"));
            
            em.persist(member);
            
            em.flush();
            em.clear();
            
            Member findMember = em.find(Member.class, member.getId());
            
            // 값 타입 조회. 컬렉션 타입은 지연 로딩
            List<Address> addressHistory = findMember.getAddressHistory();
            for (Address address : addressHistory) {
                System.out.println("address = " + address.getCity());
            }
            
            Set<String> favoriteFoods = findMember.getFavoriteFoods();
            for (String favoriteFood : favoriteFoods) {
                System.out.printl("favoriteFood = " + favoriteFood);
            }
     
        } catch (Exception e) {
            tx.rollback();
            e.printStackTrace();
        } finally {
            em.close();
        }
        emf.close();
    }
}
```

- 값 타입 조회 예제
    - 값 타입 컬렉션도 지연 로딩 전략 사용
  
```
   
// 값 타입 조회. 컬렉션 타입은 지연 로딩
List<Address> addressHistory = findMember.getAddressHistory();
for (Address address : addressHistory) {
  System.out.println("address = " + address.getCity());
}
            
Set<String> favoriteFoods = findMember.getFavoriteFoods();
for (String favoriteFood : favoriteFoods) {
  System.out.printl("favoriteFood = " + favoriteFood);
}
```
    
- 값 타입 수정 예제

```
// homeCity -> newCity
findMember.getHomeAddress().setCity("newCity"); // (X)

Address a = findMember.getHomeAddress();
findMember.setHomeAddress(new Address("newCity", a.getStreet(), a.getZipcode())); // (O)

// 치킨 -> 한식
findMember.getFavoriteFoods().remove("치킨");
findMember.getFavoriteFoods().add("한식");

findMember.getAddressHistory().remove(new Address("old1", "street", "10000"));
findMember.getAddressHistory().add(new Address("newCity1", "street", "10000"));
```

- 참고 : 값 타입 컬렉션은 영속성 전이(Cascade) + 고아 객체 제거 기능을
필수로 가진다고 볼 수 있다.
  

### 값 타입 컬렉션의 제약사항

- 값 타입은 엔티티와 다르게 식별자 개념이 없다.
- 값은 변경하면 추적이 어렵다.
- 값 타입 컬렉션에 변경 사항이 발생하면, 주인 엔티티와 연관된 모든 데이터를 삭제하고,
값 타입 컬렉션에 있는 현재 값을 모두 다시 저장한다.
  
- 값 타입 컬렉션을 매핑하는 테이블은 모든 컬럼을 묶어서 기본 키를 구성해야 함: null 입력 X, 중복 저장 X


### 값 타입 컬렉션 대안
- 실무에서는 상황에 따라 값 타입 컬렉션 대신에 일대다 관계를 고려
- 일대다 관계를 위한 엔티티를 만들고, 여기에서 값 타입을 사용
- 영속성 전이(Cascade) + 고아 객체 제거를 사용해서 값 타입 컬렉션처럼 사용
- Ex) AddressEntity

### 정리

- 엔티티 타입의 특징
  - 식별자 O
  - 생명 주기 관리
  - 공유
  
- 값 타입의 특징
  - 식별자 X
  - 생명 주기를 엔티티에 의존
  - 공유하지 않는 것이 안전(복사해서 사용)
  - 불변 객체로 만드는 것이 안전
  
- 값 타입은 정말 값 타입이라 판단될 때만 사용
- 엔티티와 값 타입을 혼동해서 엔티티를 값 타입으로 만들면 안됨
- 식별자가 필요하고, 지속해서 값을 추적, 변경해야 한다면 그것은 값 타입이 아닌 엔티티


### 실전 예제 - 값 타입 매핑
