# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 페치 조인

### 페치 조인 (fetch join)
- SQL 조인 종류 X
- JPQL에서 **성능 최적화**를 위해 제공하는 기능
- 연관된 엔티티나 컬렉션을 **SQL 한 번에 함께 조회**하는 기능
- join fetch 명령어 사용
- 페치 조인 ::=[LEFT [OUTER]|INNER] JOIN FETCH 조인 경로


### 엔티티 페치 조인
- 회원을 조회하면서 연관된 팀도 함께 조회(SQL 한번에)
- SQL을 보면 회원 뿐만 아니라 팀(T.*)도 함께 SELECT

- [JPQL]
````
select m from Member m join fetch m.team
````

- [SQL]
```
SELECT M.*, T.* FROM MEMBER M
INNER JOIN TEAM T ON M.TEAM_ID = T.ID
```

![](./image/페치조인.png)


### 페치 조인 사용 코드
````
String jpql = "select m from Member m join fetch m.team";
List<Member> members = em.createQuery(jpql, Member.class)
                            .getResultList();
for (Member member : members) {
    // 페치 조인으로 회원과 팀을 함께 조회해서 지연 로딩 X
    System.out.println("username = " + member.getUserName() + "," + 
                        "teamName = " + member.getTeam().name());
}

username = 회원 1, teamname = 팀A
username = 회원 2, teamname = 팀A
username = 회원 3, teamname = 팀B
````

### 컬렉션 페치 조인
- 일대다 관계, 컬렉션 페치 조인
- [JPQL]
```
select t
from Team t join fetch t.members
where t.name = '팀A'
```

- [SQL]
```
SELECT T.*, M.*
FROM TEAM T
INNER JOIN MEMBER M ON T.ID = M.TEAM_ID
WHERE T.NAME = '팀A'
```

![](./image/컬렉션페치조인.png)


### 컬렉션 페치 조인 사용 코드
```
String jqpl = "select t from Team t join fetch t.members where t.name = '팀A'";
List<Team> teams = em.createQuery(jpql, Team.class).getResultList();

for (Team team : teams) {
    System.out.println("teamname = " + team.getName() + ", team = " + team);
    for (Member member : team.getMembers()) {
        // 페치 조인으로 팀과 회원을 함께 조회해서 지연 로딩 발생안함
        System.out.println("-> username = " + member.getUsername() + ", member = " + member);
    }
}
```

### 페치 조인과 DISTINCT
- SQL의 DISTINCT는 중복된 결과를 제거하는 명령
- JPQL의 DISTINCT 2가지 기능 제공
    1. SQL에 DISTINCT를 추가
    2. 애플리케이션에서 엔티티 중복 제거

````
select distinct t
from Team t join fetch t.members
where t.name = '팀A'
````

- SQL에 DISTINCT를 추가하지만 데이터가 다르므로 SQL 결과에서 중복제거 실패 
- DISTINCT가 추가로 애플리케이션에서 중복 제거 시도
- 같은 식별자를 가진 Team 엔티티 제거

````
[DISTINCT 추가시 결과]
teamname = 팀A, team= Team@0x100
-> username = 회원1, member = Member@0x200
-> username = 회원2, member = Member@0x300
````


### 페치 조인과 일반 조인의 차이
- **일반 조인 실행 시 연관된 엔티티를 함께 조회하지 않음**

- [JPQL]

```
select t
from Team t join t.members m
where t.name = '연구1팀'
```

- [SQL]
```
SELECT T.*
FROM TEAM T
INNER JOIN MEMBER M ON T.ID = M.TEAM_ID
WHERE T.NAME = '연구1팀'
```
- JPQL은 결과를 반환할 때 연관관계 고려 X
- 단지 SELECT 절에 지정한 엔티티만 조회할 뿐
- 여기서는 팀 엔티티만 조회하고, 회원 엔티티는 조회 X


### 페치 조인과 일반 조인의 차이
- **페치 조인을 사용할 때만 연관된 엔티티도 함께 조회 (즉시로딩)**
- **페치 조인은 객체 그래프를 SQL 한번에 조회하는 개념**


### 페치조인 실행 예시
- 페치 조인은 연관된 엔티티를 함께 조회함
- [JPQL]
```
select t
from Team t join fetch t.members
where t.name = '연구1팀'
```

- [SQL]
```
SELECT T.*, M.*
FROM TEAM T
INNER JOIN MEMBER M ON T.ID = M.TEAM_ID
WHERE T.NAME = '연구1팀'
```