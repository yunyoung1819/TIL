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