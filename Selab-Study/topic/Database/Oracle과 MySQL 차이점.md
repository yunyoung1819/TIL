# :book: selab-study
## :pushpin: Topic. Oracle과 MySQL 차이점

### DB(Database)
- 여러 사람에 의해 공유되어 사용될 목적으로 통합하여 관리되는 데이터의 집합
- 자료를 구조화하여 저장함으로써 자료 검색과 갱신의 효율성을 높임

### Oracle
- 미국의 오라클 회사에서 제작한 세계 점유율 1위 데이터베이스 관리 시스템
- 현재 유닉스 체제에서 가장 많이 사용되는 DBMS

### Oracle 장점
- 관리시스템
  - Multiple database 튜닝이 가능함
  - 다수의 사용자가 동시에 접근이 가능
- 변화 관리
  - 변경 plan을 작성하고 실제 구현하기 전에 변경 사항의 효과를 볼 수 있음
  - 생산 시스템을 방해하지 않음
- 경고
  - 오류가 발생하면 설정되어 있는 계정 및 이메일로 연락이 옴
  - 경고는 예정된 기동 정지 시간동안 차단될 수 있음
- 분산처리
  - DBMS 실행 컴퓨터 
- 용량 처리
  - 다른 데이터베이스보다 고성능의 트랜잭션을 처리

### Oracle 단점
- 비용적인 부담
- 기능이 많아 초보자에게 어려움
- 높은 하드웨어 사양 필요


### MySQL
- 전세계적으로 가장 널리 사용되고 있는 오픈소스 데이터베이스

### MySQL 장점
- 용량&처리
  - MySQL은 오직 1MB의 RAM만 사용할 만큼 용량 차지가 적다.
- 접근성
  - 다른 데이터 관리 툴에 비해 구조가 간단하여 사용하기 쉽다.
- 가격
  - MySQL 데이터베이스는 무료라서 비용적인 부담이 적다.
  - 오픈소스는 무료, 상업용은 유료

### MySQL 단점
- 복잡한 쿼리는 성능 저하
- 트랜잭션 지원이 완벽하지 않음
- 사용자정의 함수의 사용이 쉽지 않고 유연하지 않음


### Oracle vs MySQL
- 구조적 차이
  - Oracle: DB 서버가 하나의 통합된 하나의 스토리지를 공유하는 방식
  - MySQL: DB서버마다 독립적인 스토리지를 할당하는 방식
- 조인 방식의 차이
  - Oracle: 중첩 루프 조인, 해시 조인, 소트 머지 조인 방식
  - MySQL: 중첩 루프 조인 방식 제공
- 확장성의 차이
  - Oracle: 별도의 DBMS을 설치해 사용할 수 없음
  - MySQL: 별도의 DBMS를 설치해 사용할 수 있음
- 메모리 사용률의 차이
    - Oracle: 메모리 사용율이 커서 최소 수백MB 이상이 되어야 설치 가능
    - MySQL: 메모리 사용율이 낮아서 1MB 환경에서도 설치가 가능


### 구문의 차이

- Null 값 확인 함수
```
Oracle: NVL
MySQL: IFNULL
```

- 현재 날짜 및 시간 확인 함수
```
Oracle: SYSDATE
MySQL: DATE()
```

- 날짜 포멧 변환
```
Oracle: TO_CHAR
MySQL: DATE_FORMAT
```

- 요일 변환의 숫자 범위
```
Oracle: 일,월,화,수,목,금,토를 1,2,3,4,5,6,7로 인식
MySQL: 일,월,화,수,목,금,토를 0, 1,2,3,4,5,6로 인식
```

- 문자와 문자 합치는 방법
```
Oracle: ' '
MySQL: COMCAT
```

- 형변환 방법
```
Oracle: TO_CHAR
MySQL: CAST
```

- 페이징 처리
```
Oracle: ROWNU BETWEEN 0 AND 10
MySQL: LIMIT
```


- 시퀀스 사용시 다음 번호 불러오는 방법
```
Oracle: 시퀀스명.NEXTVAL
MySQL: 시퀀스명.CURRVAL
```


### Reference
- https://velog.io/@alicesykim95/Oracle%EA%B3%BC-MySQL%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90