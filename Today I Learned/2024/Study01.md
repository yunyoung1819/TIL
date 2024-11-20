## TIL (Today I Learned)


#### JPA 성능 개선
- saveAll()은 sava 쿼리가 각각 실행됨
- JPA에서는 엔티티를 저장하면 해당 엔티티를 영속성 컨텍스트에 저장하기 위해 식별자가 필요
- Jdbc Template을 사용하여 batch Insert로 개선
- 주의점
  - JdbcTemplate을 조회 로직에서도 사용한다면 문제가 발생할 수 있음
  - JdbcTemplate은 영속성 컨텍스트를 거치지 않고 바로 DB를 조회하기 때문에 데이터에 정합성에 문제가 발생할 수 있음
  - JdbcTemplate을 사용하기 전에 영속성 컨텍스트를 flush 해서 데이터의 정합성을 보장해야함


#### MySQL5 에서 MySQL8로 마이그레이션
- MySQL 5.7의 기본 캐릭터셋은 latin1이었으나 MySQL 8에서는 기본 캐릭터셋이 utf8mb4로 변경되었음
- utf8mb4는 UTF-8의 4바이트 확장형으로 이모지나 일부 특수문자를 지원
- 기본 collation이 utf8mb4_0900_ai_ci 로 설정됨
- utf8mb4_general_ci 보다 성능과 정렬 향상도가 향상된 collation
- 특정 조회 컬럼에서 COLLATE를 명시적으로 설정해서 사용

