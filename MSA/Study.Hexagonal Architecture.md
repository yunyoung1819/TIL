## Hexagonal Architecture

### Hexagonal Project 패키기 구조 설계

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


### 멤버십 서비스 정의, DB 설계
- 멤버십 서비스
  - fastcampus-pay 라는 비즈니스에서 제공하는 멤버십 서비스로서, 패캠 페이에 가입하는 개인/법인 고객의 정보를 소유(ownership)하고 관련 정보의 변경에 대한 의무를 가진 서비스