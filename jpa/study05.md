## 영속성 컨텍스트1


### JPA에서 가장 중요한 2가지

- 객체와 관계형 데이터베이스 매핑하기 (Object Relational Mapping)
- 영속성 컨텍스트 


### 엔티티 매니저 팩토리와 엔티티 매니저

![엔티티매니저팩토리](./image/엔티티매니저팩토리.png)


### 영속성 컨텍스트

- JPA를 이해하는데 가장 중요한 용어
- "엔티티를 영구 저장하는 환경" 이라는 뜻
- EntityManager.persist(entity);


### 엔티티 매니저? 영속성 컨텍스트?

- 영속성 컨텍스트는 논리적인 개념
- 눈에 보이지 않는다.
- 엔티티 매니저를 통해서 영속성 컨텍스트에 접근 


### 엔티티의 생명주기

- 비영속 (new/transient)
    - 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태
- 영속 (managed)
    - 영속성 컨텍스트에 관리되는 상태
- 준영속 (detached)
    - 영속성 컨텍스트에 저장되었다가 분리된 상태
- 삭제 (removed)
    - 삭제된 상태


![엔티티생명주기](./image/엔티티생명주기.png)


### 비영속

````
// 객체를 생성한 상태 (비영속)

Member member = new Member();
member.setId("member1");
member.setUsername("회원1");
````


### 영속

````
// 객체를 저장한 상태 (영속)
em.persist(member);
````


### 준영속

````
// 회원 엔티티를 영속성 컨텍스트에서 분리, 준영속 상태
em.detach(member);
````


### 객체를 삭제한 상태 (삭제)

````
em.remove(member);
````


### 영속성 컨텍스트의 이점

- 1차 캐시
- 동일성(identity) 보장
- 트랜잭션을 지원하는 쓰기 지연 (transactional write-behind)
- 변경 감지 (Dirty Checking)
- 지연 로딩 (Lazy Loading)


### 엔티티 조회, 1차 캐시 

````
// 엔티티를 생성한 상태 (비영속)
Member member = new Member();
member.setId("member1");
member.setUsername("회원1");

// 엔티티를 영속
em.persist(member);
````

### 1차 캐시에서 조회

````
Member member = new Member();
member.setId("member");
member.setUsername("회원1");

// 1차 캐시에 저장됨
em.persist(member);

// 1차 캐시에서 조회
Member findMember = em.find(Member.class, "member1");
````


![1차캐시](./image/1차캐시.png);


### 데이터베이스에서 조회

````
Member findMember2 = em.find(Member.class, "member2");
````

> 1. find("member2")    // 1차 캐시에 없음
> 2. DB 조회
> 3. 1차 캐시에 저장
> 4. 반환  