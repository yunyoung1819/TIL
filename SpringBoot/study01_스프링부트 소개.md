# :book: 스프링 부트 개념과 활용 (백기선) 

## :pushpin: 스프링 부트 소개

### 스프링 부트
- 제품 수준의 스프링 애플리케이션을 만들 때 빠르고 쉽게 만들 수 있게 도와줌

### 스프링 부트 프로젝트 구조
- 메이븐 기본 프로젝트 구조와 동일
    - 소스 코드 (src\main\java)
    - 소스 리소스 (src\main\resource)
    - 테스트 코드 (src\test\java)
    - 테스트 리소스 (src\test\resource)
    
- 메인 애플리케이션 위치
    - 기본 패키지
  
### 자동 설정 개요
- **@EnableAutoConfiguration** (@SpringBootApplication 안에 숨어 있음)
- 빈은 사실 두 단계로 나눠서 읽힘
  - 1단계: **@ComponentScan**
  - 2단계: **@EnableAutoConfiguration**
  
- **@ComponentScan**
  - @Component
  - @Configuration @Repository @Service @Controller @RestController
  
- **@EnableAutoConfiguration**
  - spring.factories
    - org.springframework.boot.autoconfigure.EnableAutoConfiguration
  - @Configuration
  - @ConditionOnXxxYyyZzz
  

### @SpringBootApplication
- **@SpringBootApplication**은 아래 3가지 애노테이션을 하나로 합친 것과 같다.
  - @Configuration
  - @ComponentScan
  - @EnableAutoConfiguration
