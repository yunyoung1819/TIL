# :book: 스프링 핵심 원리

## :pushpin: 중복 등록과 충돌

### 중복 등록과 충돌
- 컴포넌트 스캔에서 같은 빈 이름을 등록하면 어떻게 될까?
- 다음 두가지 상황이 있다.

1. 자동 빈 등록 vs 자동 빈 등록
2. 수동 빈 등록 vs 자동 빈 등록

### 자동 빈 등록 vs 자동 빈 등록
- 컴포넌트 스캔에 의해 자동으로 스프링 빈이 등록되는데, 그 이름이 같은 경우 스프링은 오류를 발생시킨다.
    - `ConflictingBeanDefinitionException` 예외 발생 
    
### 수동 빈 등록 vs 자동 빈 등록
- 만약 수동 빈 등록과 자동 빈 등록에서 빈 이름이 충돌되면 어떻게 될까?

```java
@Component
public class MemoryMemberRepository implements MemberRepository {}
```

````java
@Configuration
@ComponentScan(
        excludeFilters = @Fileter(type = FilterType.ANNOTATION, classes = Configuration.class)
)
public class AutoAppConfig {
    
    @Bean(name = "memoryMemberRepository") 
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
````

- 이 경우 수동 빈 등록이 우선권을 가진다. (수동 빈이 자동 빈을 오버라이딩 해버린다)

- 수동 빈 등록시 남는 로그
```
Ovverriding bean definition for bean 'memoryMemberRepository' with a different definition: replacing
```

- 물론 개발자가 의도적으로 이런 결과를 기대했다면, 자동보다는 수동이 우선권을 가지는 것이 좋다. 하지만 현실은 개발자가 의도적으로 설정해서 
이런 결과가 만들어지기보다는 여러 설정들이 꼬여서 이런 결과가 만들어지는 경우가 대부분이다!
  
- 그러면 정말 잡기 어려운 버그가 만들어진다. 항상 잡기 어려운 버그는 애매한 버그다.
- 그래서 최근 스프링 부트에서는 수동 빈 등록과 자동 빈 등록이 충돌나면 오류가 발생하도록 기본 값을 바꾸었다.

- 수동 빈 등록, 자동 빈 등록 오류시 스프링 부트 에러
```
Consider renaming one of the beans or enabling overriding by setting spring.main.allow-bean-definition-overriding=true
```