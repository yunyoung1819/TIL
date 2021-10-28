# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 값 타입

### 값 타입의 비교

- 값 타입: 인스턴스가 달라도 그 안에 값이 같으면 같은 것으로 봐야함

```
int a = 10;
int b = 10;
```

```
Address a = new Address("기흥구")
Address b = new Address("기흥구")
```

```
public class ValueMain {
    
    public static void main(String[] args) {
        
        int a = 10;
        int b = 10;
        
        System.out.println("a == b: " + (a == b));
        
        Address address1 = new Address("city", "street", "10000:);
        Address address2 = new Address("city", "street", "10000:);
        
        System.out.println("address1 == address2: " + (address1 == adrress2));
    }
}
```

```
a == b: true
address1 == address2: false 
```

### 값 타입의 비교

- **동일성(identity) 비교**: 인스턴스의 참조 값을 비교, == 사용
- **동등성(equivalence) 비교**: 인스턴스의 값을 비교, equals() 사용
- 값 타입은 a.equals(b)를 사용해서 동등성 비교를 해야 함
- 값 타입의 equals() 메소드를 적절하게 재정의 (주로 모든 필드 사용)

```
public class Address {
    ...
    
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Address address = (Address) o;
        return Objecs.equals(city, addrss.city) &&
                Objects.equals(street, address.street) &&
                Objects.equals(zipcode, address.zipcode);
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(city, street, zipcode);
    }
}
```

```
a == b: true
address1 == address2: true 
```