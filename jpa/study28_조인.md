# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 조인

### 조인

#### 내부 조인 
- SELECT m FROM Member m [INNER] JOIN m.team t

#### 외부 조인
- SELECT m FROM Member m LEFT [OUTER] JOIN m.team t

#### 세타 조인
- select count(m) from Member m, Team t where m.username = t.name


### 조인 - ON 절

- ON 절을 활용한 조인 (JPA 2.1부터 지원)
    1. 조인 대상 피러링
    2. 연관관계 없는 엔티티 외부 조인(하이버네이트 5.1부터)
    