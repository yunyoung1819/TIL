# :book: 백엔드 개발자를 위한 한 번에 끝내는 대용량 데이터 & 트래픽 처리
## :pushpin: 대용량 처리를 위한 MySQL 이해
### 실습 환경 구축

### 사용 기술
- MySQL, Spring, Jdbc Template, EasyRandom

### 대용량 서버를 구축하기 위해서는 어떤 것들을 알아야할까
- Spring, MySQL, MongoDB, Redis, Kafka, MSA, ...
- 서버 개발자의 핵심은 데이터다.
- 대용량 시스템이 어려운 이유는 결국 많은 양의 `데이터`에서 시작된다.
- 어떻게 많은 양의 데이터를 안정적으로 `삽입`, `갱신`, `조회`할 것이냐?
  - 정규화, 인덱스, 트랜잭션, 동시성 제어

### 실습 환경 구축
1. brew 설치하기
2. MySQL 설치
   - 터미널 창에서 아래 커맨드 입력
   - brew install mysql@8.0
3. mysql 실행
````
brew services start mysql
````
4. mysql 상태 확인
````
brew services list
````
5. mysql 콘솔 접속
````
mysql -uroot
mysql -uroot -p // 비밀번호 설정 시
````
6. mysql 데이터베이스 생성
```text
CREATE DATABASE fast_sns;
```
7. mysql 데이터베이스 확인
````
SHOW DATABASES;
````
8. mysql 콘솔 종료
````
exit
````