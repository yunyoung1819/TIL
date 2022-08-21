## JPA 시작하기

### H2 데이터베이스 설치와 실행

- http://www.h2database.com
- 최고의 실습용 DB
- 가볍다 (1.5M)
- 웹용 쿼리툴 제공
- MySQL, Oracle 데이터베이스 시뮬레이션 기능
- 시퀀스, AUTO INCREMENT 기능 지원


### 메이븐 

- https://maven.apache.org/
- 자바 라이브러리, 빌드 관리
- 라이브러리 자동 다운로드 및 의존성 관리
- 최근에는 그래들(Gradle)이 점점 유명 


### JPA 설정하기 - persistence.xml

- JPA 설정 파일
- /META-INF/persistence.xml 위치
- persistence-unit name으로 이름 지정
- **javax.persistence로 시작 : JPA 표준 속성**
- **hibernate로 시작 : 하이버네이트 전용 속성**


### 데이터베이스 방언

- JPA는 특정 데이터베이스에 종속 X
- 각각의 데이터베이스가 제공하는 SQL 문법과 함수는 조금씩 다름
    - 가변 문자: MySQL은 VARCHAR, Oracle은 VARCHAR2
    - 문자열을 자르는 함수 : SQL 표준은 SUBSTRING(), Oracle은 SUBSTR()
    - 페이징: MySQL은 LIMIT, Oracle은 ROWNUM
- 방언 : SQL 표준을 지키지 않는 특정 데이터베이스만의 고유한 기능  
- hibernate.dialect 속성에 지정
    - H2: org.hibernate.dialect.H2Dialect
    - Oracle 10g: org.hibernate.dialect.Oracle10gDialect
    - MySQL: org.hibernate.dialect.MySQL5InnoDBDialect
- 하이버네이트는 40가지 이상의 데이터베이스 방언 지원
