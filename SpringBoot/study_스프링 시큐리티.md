# :book: 스프링 부트 개념과 활용 (백기선)

## :pushpin: 스프링 시큐리티: spring-boot-starter-security

### 스프링 시큐리티
- 웹 시큐리티
- 메소드 시큐리티
- 다양한 인증 방법 지원
    - LDAP, 폼 인증, Basic 인증, OAuth, ...
    
### 스프링 부트 시큐리티 자동 설정
- SecurityAutoConfiguration
- UserDetailsServiceAutoConfiguration
- spring-boot-starter-security
    - 스프링 시큐리티 5.* 의존성 추가
    
- 모든 요청에 인증이 필요함
- 기본 사용자 생성
    - Username: user
    - Password: 애플리케이션을 실행할 때마다 랜덤 값 생성 (콘솔에 출력됨)
      - ex: 2f0f2392-8169-4526-a155-6fbef5de9a4a
    - spring.security.user.name
    - spring.security.user.password
    
- 인증 관련 각종 이벤트 발생
    - DefaultAuthenticationEventPublisher 빈 등록
    - 다양한 인증 에러 핸들러 등록 가능
  

### 스프링부트 시큐리티 테스ㅌ,

```
<dependency>
  <groupId>org.springframework.security</groupId>
  <artifactId>spring-security-test</artifactId>
  <version>${spring-security.version}</version>
  <scope>test</scope>
</dependency>
```

```
@RunWith(SpringRunner.class)
@WebMvcTest(HomeController.class)
public class HomeControllerTest {

    @Autowired
    MockMvc mockMvc;

    @Test
    @WithMockUser
    public void hello() throws Exception {
        mockMvc.perform(get("/hello"))
                .andDo(print())
                .andExpect(status().isOk())
                .andExpect(view().name("hello"));
    }

    @Test
    public void hello_without_user() throws Exception {
        mockMvc.perform(get("/hello"))
                .andDo(print())
                .andExpect(status().isUnauthorized());
    }

    @Test
    @WithMockUser
    public void my() throws Exception {
        mockMvc.perform(get("/my"))
                .andDo(print())
                .andExpect(status().isOk())
                .andExpect(view().name("my"));
    }
}
```