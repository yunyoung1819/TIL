## :pushpin: EDA 기반 microservice 구현 (with Hexagonal, DDD)

### 도메인 모델 테스트 
- 테스트 시나리오 구상해보기
  - 도서샘플 1,2 생성
  - 도서 1,2 대여
  - 도서 1 반납
  - 도서 2 강제연체 처리 -> 대여정지됨
  - 도서 2 반납 -> 연체료 계산됨
  - 정지해제처리 -> 포인트로 연체료 삭감

### 외부 영역 구현 (프레임워크 헥사곤)
- JPA 어댑터 구현
  - OR 매핑 설정
    - 이론과 현실
      - 도메인 모델(POJO)에 OR 매핑을 하는 것은 도메인을 기술에 오염시키는 것
      - 도메인 모델이 데이터 영역과 관련된 이유로 변경되어야할 수도 있음 (단일 책임 원칙 위배)
      - 그러나 OR 매핑을 위한 별도의 영속성 모델을 만드는 것은 너무 많은 보일러 플레이트 코드를 양산함. 매핑 구현에 상당한 노력 필요 (개발을 불필요하게 더디게 함)
      - 비즈니스와 팀 성숙도에 따라 그때그때 다를 수 있다
    - 타협의 필요성
      - 단순하고 복잡하지 않은 유스케이스라면 도메인 모델에 OR 매핑을 처리하는 것에서 시작하는 것이 좋음
    - 도메인 모델 vs 데이터 모델 매핑
    - 도메인 모델 (객체 모델)