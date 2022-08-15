# :book: 실전! 스프링 부트와 JPA 활용

## :pushpin: 살전! 스프링 부트와 JPA 활용

### gradle 의존관계 보기
```
./gradlew dependencies
```

### 스프링 부트 라이브러리
- spring-boot-starter-web
  - spring-boot-starter-tomcat: 톰캣 (웹서버)
  - spring-webmvc: 스프링 웹 MVC
  
- spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View)

- spring-boot-starter-data-jpa
  - spring-boot-starter-aop
  - spring-boot-starter-jdbc
    - HikariCP 커넥션 풀 (부트 2.0 기본)
  - hibernate + JPA: 하이버네이트 + JPA
  - spring-data-jpa: 스프링 데이터 JPA

- spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
  - spring-boot
    - spring-core
  - spring-boot-starter-logging
    - logback, slf4j

### 테스트 라이브러리
- spring-boot-starter-test
  - junit: 테스트 프레임워크
  - mockito: 목 라이브러리
  - assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
  - spring-test: 스프링 통합 테스트 지원
  

### View 환경 설정
- thymeleaf 템플릿 엔진 
- 스프링 부트 thymeleaf viewName 매핑
  - resources:`templates`/ + {ViewName} + `.html`

### H2 데이터베이스 설치
- 개발이나 테스트 용도로 가볍고 편리한 DB, 웹 화면 제공
- https://www.h2database.com
- 다운로드 및 설치 (1.4.99)
- 데이터베이스 파일 생성 방법
  - http://localhost:8082 접속
  - jdbc:h2:~/jpashop (최소 한번, 세션키 유지한 상태로 실행)
  - ~/jpashop.mv.db 파일 행성 확인
  - 이후부터는 Jdbc:h2:tcp://localhost/~/jpashop 이렇게 접속

### JPA와 DB 설정, 동작 확인

- main/resources/application.yml

```
spring:
  datasource:
#
  url: jdbc:h2:tcp://localhost/~/jpashop
  username: sa
  password:
  driver-class-name: org.h2.Driver
jpa:
  hibernate:
    ddl-auto: create
  properties:
    hibernate:
       show_sql: true
      format_sql: true
    logging.level:
      org.hibernate.SQL: debug
    #  org.hibernate.type: trac
```

- spring.jpa.hibernate.ddl-auto: create
  - 이 옵션은 애플리케이션 실행 시점에 테이블을 drop하고 다시 생성한다.

- 참고: 모든 로그 출력은 가급적 로거를 통해 남겨야 한다.
- show_sql: 옵션은 System.out 에 하이버네이트 실행 SQL을 남긴다.
- org.hibernate.SQL 옵션은 logger를 통해 하이버네이트 실행 SQL을 남긴다.
- 주의: application.yml 같은 yml 파일은 띄어쓰기(스페이스) 2칸으로 계층을 만든다. 따라서 띄어쓰기 2칸을 필수로 적어주어야 한다.
- 예를 들어 datasource는 spring 하위에 있고 앞에 띄어쓰기 2칸이 있으므로 spring.datasource가 된다.
- 스프링부트를 통해 복잡한 설정이 다 자동화되었다. persistence.xml 도 없고 LocalContainerEntityManagerFactoryBean도 없다.


### 쿼리 파라미터 로그 남기기