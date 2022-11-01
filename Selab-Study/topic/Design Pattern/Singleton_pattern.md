# :book: selab-study
## :pushpin: Topic. 싱글톤 패턴 (Singleton Pattern)


> 애플리케이션이 시작될 때, 어떤 클래스가 최초 한 번만 메모리를 할당(static)하고 
> 해당 메모리에 인스턴스를 만들어 사용하는 패턴


- 객체의 인스턴스가 오직 1개만 생성되는 패턴
- 즉 싱글톤 패턴은 하나의 인스턴스만 생성하여 사용하는 디자인 패턴
- 인스턴스가 필요할 때, 똑같은 인스턴스를 만들지 않고 기존의 인스턴스를 활용하는 것
- java에서는 생성자를 `private`으로 선언해 다른 곳에서 생성하지 못하도록 만들고 `getInstance()` 메서드를 통해 받아서 사용하도록 구현함


### 싱글톤을 사용하는 이유

- 객체를 생성할 때마다 메모리 영역을 할당받아야 함.
- 하지만 한 번의 `new`를 통해 객체를 생성한다면 **메모리 낭비를 방지**할 수 있음
- 싱글톤으로 구현한 인스턴스는 전역이므로 다른 클래스의 인스턴스들이 **데이터를 공유하다는 것이 가능**하다는 장점이 있음
- 하지만 여러 클래스의 인스턴스에서 싱글톤 인스턴스의 데이터에 동시에 접근하게 되면 **동시성 문제**가 발생할 수 있으니 이 점을 유의해서 설계 필요
- 도메인 관점에서 인스턴스가 한 개만 존재하는 것을 보증하고 싶을 때도 싱글톤 패턴을 사용


### 싱글톤 패턴의 문제점
- 싱글톤 패턴을 구현하는 코드 자체가 많이 필요함
- 멀티스레딩 환경에서 발생할 수 있는 동시성 문제 해결을 위해 `syncronized` 키워드를 사용해야 함
- 테스트하기 어렵다는 단점이 있음
- 의존 관계상 클라이언트가 구체 클래스에 의존. new 키워드를 직접 사용하여 클래스 안에서 객체를 생성하고 있으므로,
SOLID 원칙 중 DIP를 위반하게 되고 OCP 원칙 또한 위반할 가능성이 높음 
- 스프링 컨테이너 같은 프레임워크의 도움을 받으면 싱글톤 패턴의 문제점들을 보완하면서 장점의 혜택은 누릴 수 있음


### 예제 코드

- 객체는 private static으로 선언해서 오로지 한 번만 생성하도록 구현
- 생성자는 private으로 선언

```java
public class Company {

    private static Company instance = new Company();

    private Company() {
        // 생성자는 외부에서 호출하지 못하게 private으로 지정해야 한다.
    }

    public static Company getInstance() {
        if (instance == null) {
        	instance = new Company();
        }
        return instance;
    } 
}
```


```java
public class SingletonTest {

    public static void main(String[] args) {
        Company company1 = Company.getInstance();
        Company company2 = Company.getInstace();
    
        System.out.println(company1);
        System.out.println(company2);

    } 
}
```