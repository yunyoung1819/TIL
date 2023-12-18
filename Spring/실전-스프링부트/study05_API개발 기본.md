# :book: 실전! 스프링 부트와 JPA 활용

## :pushpin: 살전! 스프링 부트와 JPA 활용 2편

### :seedling: API 개발 기본

### 회원 조회 API
회원조회 V1: 응답값으로 엔티티를 직접 외부에 노출

```text
@RestController
@RequiredArgsConstructor
public class MemberApiController {
    private final MemberService memberService;
    
    @GetMapping("/api/v1/members")
    public List<Member> membersV1() {
        return memberService.findMembers();
    }
}
```

회원조회 V1: 응답값으로 엔티티를 직접 외부에 노출
문제점
- 엔티티에 프레젠테이션 계층을 위한 로직이 추가됨
- 기본적으로 엔티티의 모든 값이 노출됨
- 응답 스펙을 맞추기 위해 로직이 추가됨 (@JsonIgnore, 별도의 뷰 로직 등등)
- 실무에서는 같은 엔티티에 대해 API가 용도에 따라 다양하게 만들어지는데, 한 엔티티에 각각의 API를 위한 프레젠테이션 응답 로직을 담기는 어려움
- 엔티티가 변경되면 API 스펙이 변함 
- 추가로 컬렉션을 직접 반환하면 향후 API 스펙을 변경하기 어려움 (별도의 Result 클래스 생성으로 해결)
- 결론: API 응답 스펙에 맞추어 별도의 DTO를 반환한다.