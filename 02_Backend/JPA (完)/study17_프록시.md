# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 프록시와 연관관계 관리

### 프록시

- Member를 조회할 때 Team도 함께 조회해야 할까?

![프록시](image/proxy1.png)

- 회원과 팀 함께 출력
````
public void printUserAndTeam(String memberId) {
    Member member = em.find(Member.class, memberId);
    Team team = member.getTeam();
    System.out.println("회원 이름: " + member.getUsername());
    System.out.println("소속팀: " + team.getName());
}
````

- 회원만 출력
````
public void printUser(String memberId) {
    Member member = em.find(Member.class, memberId);
    Team team = member.getTeam();
    System.out.println("회원 이름: " + member.getUsername());
}
````


### 프록시 기초

- em.find() vs em.getReference()
- em.find(): 데이터베이스를 통해서 실제 엔티티 객체 조회
- em.getReference(): 데이터베이스 조회를 미루는 가짜(프록시) 엔티티 객체 조회. 
  em.getReference()를 호출하는 시점에는 데이터베이스에 쿼리가 실행되지 않음.
값이 실제 사용되는 시점에 시점에 쿼리를 실행함
  
![프록시2](image/proxy2.png)


### 프록시 특징 (1)
- 실제 클래스를 상속받아 만들어짐
- 실제 클래스와 겉 모양이 같다.
- 사용하는 입장에서 진자 객체인지 프록시 객체인지 구분하지 않고 사용하면 됨 (이론상)
- 프록시 객체는 실제 객체의 참조(target)를 보관
- 프록시 객체를 호출하면 프록시 객체는 실제 객체의 메소드 호출

![프록시4](image/proxy4.png)


### 프록시 객체의 초기화

````
Member member = em.geetReference(Member.class, "id1");
member.getName();
````

![프록시5](image/proxy5.png)


### 프록시 특징 (2)
- 프록시 객체는 처음 사용할 때 한번만 초기화
- 프록시 객체를 초기화할 떄, 프록시 객체가 실제 엔티티로 바뀌는 것은 아님, 초기화되면 프록시 객체를 통해서 실제 엔티티에 접근 가능
- 프록시 객체는 원본 엔티티를 상속받음. 따라서 타입 체크시 주의해야함(== 비교 실패, 대신 instance of 사용)
- 영속성 컨텍스트에 찾는 엔티티가 이미 있으면 em.getReference()를 호출해도 실제 엔티티 반환
- 영속성 컨텍스트의 도움을 받을 수 없는 준영속 상태일 때, 프록시를 초기화하면 문제 발생
  (하이버네이트는 org.hibernate.LazyInitializationException 예외)

  
### 프록시 확인
- 프록시 인스턴스의 초기화 여부 확인
  - PersistenceUnitUtil.isLoaded(Object entity)

- 프록시 클래스 확인 방법
  - entity.getClass().getName() 출력 (..javasist.. or HibernateProxy ..)

- 프록시 강제 초기화
  - org.hibernate.Hibernate.initialize(entity);
  
- 참고: JPA 표준은 강제 초기화 없음
  - 강제 호출 : member.getName()