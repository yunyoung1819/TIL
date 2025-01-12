## 실습1: Hexagonal Architecture

## 01. Spring Boot 개발 환경 세팅, Hexagonal 아키텍쳐

## 02. JPA와 Hexagonal 아키텍처
- Hexagonal Project 패키기 구조 설계

````
fastcampus-pay
    - membership-service
        - src.main
            - java
                - com.fastcampuspay.membership // 각 서비스 별 최상위 패키지
                    - adapter   // adapter는 외부 시스템과의 상호 작용
                        - in.web
                        - out.persistence
                    - application
                        - port      // port는 비즈니스 로직(app)과 직접 통신하는 인터페이스
                            - in
                            - out
                        - service   // service 는 port 인터페이스의 실제 비즈니스 로직의 구현체
                    - domain        // domain은 일반적인 모델 정보를 저장하는 패키지
                - build.gradle
            - test
````


### MVP 버전의 Membership Service 정의하기

- 멤버십 서비스 
  - fastcampus-pay (이하, 패캠 페이)라는 비즈니스에서 제공하는 멤버십 서비스로서, 패캠 페이에 가입하는 개인/법인 고객의 정보를 
  소유(ownership)하고 관련 정보의 변경에 대한 의무를 가진 서비스

- MVP Version
  - fastcampus-pay (이하, 패캠 페이)라는 비즈니스에서 제공하는 멤버십 서비스로서, 패캠 페이에 가입하는
  개인/법인 고객의 정보를 소유(ownership)하고 새로운 멤버십(개인/법인)의 추가가 가능하며 이에 대한 정보를 조회할 수 있는 기능을 제공하는 서비스


## 03. JPA와 Hexagonal 아키텍처를 활용한 고객 서비스 개발 2
### API 설계
- Query
  - 고객 정보(그중에서도 membershipId)를 통한 고객 정보의 조회
  - find - membership (by membershipId)
  - Request Params: membershipId
  - Response: Membership (membershipId, name, addr, ...)

- Command
  - 필요한 고객 정보를 통한 신규 고객 멤버십의 생성
  - register - membershipId
  - Request Params: Membership (membershipId, name, addr, ...)
  - Response: Registered Membership With Response Code (200, 400, 500, ...)
