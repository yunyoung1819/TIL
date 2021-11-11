# :book: 스프링 부트 개념과 활용 (백기선)

## :pushpin: 자동 설정 만들기

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


### 자동 설정 구현 1부
- Xxx-Spring-Boot-Autoconfigure 모듈: 자동 설정
- Xxx-Spring-Boot-Starter 모듈: 필요한 의존성 정의
- 그냥 하나로 만들고 싶을 때는?
    - Xxx-Spring-Boot-Starter

### 구현 방법
1. 의존성 추가

```
<dependencies>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-autoconfigure</artifactId>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-autoconfigure-processor</artifactId>
       <optional>true</optional>
   </dependency>
</dependencies>
<dependencyManagement>
   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-dependencies</artifactId>
           <version>2.0.3.RELEASE</version>
           <type>pom</type>
           <scope>import</scope>
       </dependency>
   </dependencies>
</dependencyManagement>
```

2. @Configuration 파일 작성
3. src/main/resource/META-INF 에 spring.factories 파일 만들기
4. spring.factories 안에 자동 설정 파일 추가

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
me.young.HolomanConfiguration
```

5. mvn install


### 자동 설정 만들기 2부
- 덮어쓰기 방지하기
  - @ConditionalOnMissingBean
  
- 빈 재정의 수고 덜기
  - @ConfigurationProperties("holoman")
  - @EnableConfigurationProperties(HolomanProperties)
  - 프로퍼티 키값 자동 완성
  
```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-configuration-processor</artifactId>
  <optional>true</optional>
</dependency>
```
