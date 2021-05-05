# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 즉시 로딩과 지연 로딩

### Member를 조회할 때 Team도 함께 조회해야 할까?

- 단순히 member 정보만 사용하는 비즈니스 로직
- println(member.getName());

![스크린샷1](./image/스크린샷1.png)


### 지연 로딩 LAZY을 사용해서 프록시로 조회

```
@Entity
public class Member {
    
    @Id
    @GeneratedValue
    private Long id;
    
    @Column(name = "USERNAME")
    private String name;
    
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "TEAM_ID")
    private Team team;
    
    ...
}
```