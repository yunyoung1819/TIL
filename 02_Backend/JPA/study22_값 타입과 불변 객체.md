# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 값 타입과 불변 객체

### 값 타입과 불변 객체

- 값 타입은 복잡한 객체 세상을 조금이라도 단순화하려고 만든 개념이다.
따라서 값 타입은 단순하고 안전하게 다룰 수 있어야 한다.
  

### 값 타입 공유 참조

- 임베디드 타입 같은 값 타입을 여러 엔티티에서 공유하면 위험함
- 부작용(side effect) 발생

### 값 타입 복사

- 값 타입의 실제 인스턴스인 값을 공유하는 것은 위험
- 대신 값(인스턴스)를 복사해서 사용

```
Address address = new Address("city", "street", "10000");

Member member = new Member();
member.setUsername("member1");
member.setHomeAddress(address);
em.persist(member);

Address copyAddress = new Address(address.getCity(), address.getStreet(), address.getZipCode());

Member member2 = new Member();
member2.setUsername("member2");
member2.setHomeAddress(copyAddress);
em.persist(member2);

// 비즈니스 로직
member.getHomeAddress().setCity("newCity");

```

### 객체 타입의 한계

- 항상 값을 복사해서 사용하면 공유 참조로 인해 발생하는 부작용을 피할 수 있다.
- 문제는 임베디드 타입처럼 직접 정의한 값 타입은 자바의 기본 타입이 아니라 객체 타입이다.
- 자바 기본 타입에 값을 대입하면 값을 복사한다.
- 객체 타입은 참조 값을 직접 대입하는 것을 막을 방법이 없다.
- 객체의 공유 참조는 피할 수 없다.

### 객체 타입의 한계

- 기본 타입(primitive type)

```
int a = 10;
int b = a;  // 기본 타입은 값을 복사
b = 4;
```

- 객체 타입
````
Address a = new Address("Old");
Address b = a;  // 객체 타입은 참조를 전달
b.setCity("New")
````

### 불변 객체

- 객체 타입을 수정할 수 없게 만들면 부작용을 원천 차단
- 값 타입은 불변 객체(immutable object)로 설계해야함
- **불변 객체: 생성 시점 이후 절대 값을 변경할 수 없는 객체**
- 생성자로만 값을 설정하고 수정자(Setter)를 만들지 않으면 됨
- 참고: Integer, String은 자바가 제공하는 대표적인 불변 객체

```
@Embeddable
public class Address {
    private String city;
    private String street;
    private String zipcode;
    
    public Address() {
    }
    
    public Address(String city, String street, String zipcode) {
        this.city = city;
        this.street = street;
        this.zipcode = zipcode;
    }
    
    public String getCity() { return city; }
    public String getStreet() { return street; }
    public String zipcode() { return zipcode; }
}
```

```
member.getHomeAddress().setCity("newCity") // 에러. 값을 변경할 수 없음
```

> 불변이라는 작은 제약으로 부작용이라는 큰 재앙을 막을 수 있다.