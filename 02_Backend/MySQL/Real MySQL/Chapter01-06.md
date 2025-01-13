# :book: Real MySQL

## :pushpin: Chapter 01. 소개

### MySQL 소개 
- MySQL은 소스가 공개된 오픈소스 데이터베이스

### 왜 MySQL인가?
- MySQL과 오라클을 비교해본다면 당연히 MySQL의 경쟁력은 가격이나 비용일 것이다.

---

## :pushpin: Chapter 02. 설치와 설정 
- MySQL 서버가 설치된 디렉터리는 `/usr/local/mysql` 이며 하위의 각 디렉토리의 정보는 다음과 같다.
  - bin: MySQL 서버와 클라이언트 프로그램, 유틸리티를 위한 디렉터리
  - data: 로그 파일과 데이터 파일들이 저장되는 디렉터리
  - include: C/C++ 헤더 파일들이 저장된 디렉터리
  - lib: 라이브러리 파일들이 저장된 디렉터리
  - share: 다양한 지원 파일들이 저장돼 있으며, 에러 메시지나 샘플 설정 파일(my.cnf)이 있는 디렉터리

### MySQL 8.0 업그레이드 시 고려 사항
- 사용자 인증 방식 변경
- MySQL 8.0과의 호환성 체크
- 외래키 이름의 길이
  - MySQL 8.0에서는 외래키(Foreign Key)의 이름이 64글자로 제한
- 인덱스 힌트
- GROUP BY에 사용된 정렬 옵션
- 파티션을 위한 공용 테이블스페이스

### 서버 설정
- 일반적으로 MySQL 서버는 단 하나의 설정 파일을 사용
- 리눅스를 포함한 유닉스 계열에서는 my.cnf
- 윈도우 계열에서는 my.ini

만약 설치된 MySQL 서버가 어느 디렉터리에서 my.cnf 파일을 읽는지 궁금하다면?
```shell
mysqld --verbose --help
```

### 시스템 변수
- MySQL 서버는 기동하면서 설정 파일의 내용을 읽어 메모리나 작동 방식을 초기화하고 접속된 사용자를 제어하기 위해 이러한 값을 별도로 저장해둠
- 이렇게 저장된 값을 시스템 변수(System Variables)라고 함

```shell
SHOW GLOBAL VARIABLES;
```

---
## :pushpin: Chapter 04. 아키텍처 

### MySQL 엔진 아키텍처
- MySQL 서버는 사람의 머리 역할을 담당하는 MySQL 엔진과 손발 역할을 담당하는 스토리지 엔진으로 구분
- 이 둘을 모두 합쳐서 그냥 MySQL 또는 MySQL 서버라고 표현함

### MySQL 엔진
- MySQL 엔진은 클라이언트로부터의 접속 및 쿼리 요청을 처리하는 커넥션 핸들러와 SQL 파서 및 전처리기, 쿼리의 최적화된 실행을 위한 옵티마이저가 중심
- MySQL은 표준 SQL(ANSI SQL) 문법을 지원하기 때문에 표준 문법에 따라 작성된 쿼리는 타 DBMS와 호환되어 실행될 수 있음

### 스토리지 엔진
- MySQL 엔진: 요청된 SQL 문장을 분석하거나 최적화하는등 DBMS의 두뇌에 해당하는 처리를 수행
- 스토리지 엔진: 실제 데이터를 디스크 스토리지에 저장하거나 디스크 스토리지로부터 데이터를 읽어오는 부분을 전담

### 핸들러 API
- 쿼리 실행기에서 데이터를 쓰거나 읽어야할 때는 각 스토리지 엔진에 쓰기 또는 읽기를 요청. 이러한 요청을 핸들러(Handler) 요청이라고 함
- 여기서 사용되는 API를 핸들러 API라고 함

### MySQL 스레딩 구조
- MySQL 서버는 프로세스 기반이 아니라 스레드 기반으로 작동
  - 포그라운(Foreground) 스레드
  - 백그라운드(Backgroud) 스레드
- 실행 중인 스레드의 목록은 performance_schema 데이터베이스의 threads 테이블에서 확인
- 동일한 이름의 스레드가 2개 이상씩 보이는 것은 여러 스레드가 동일 작업을 병렬로 처리하는 경우

```sql
select thread_id, name, type, processlist_user, processlist_host from performance_schema.threads order by type, thread_id;
```

### 포그라운드 스레드(클라이언트 스레드)
- 최소한 MySQL 서버에 접속된 클라이언트의 수만큼 존재하며 주로 각 클라이언트 사용자가 요청하는 쿼리 문장을 처리
- thread_cache_size

### 백그라운드 스레드 
- InnoDB는 다음과 같은 여러가지 작업이 백그라운드로 처리됨
  - 인서트 버퍼를 병합하는 스레드
  - 로그를 디스크로 기록하는 스레드
  - InnoDB 버퍼 풀의 데이터를 디스크에 기록하는 스레드
  - 데이터를 버퍼로 읽어오는 스레드
  - 잠금이나 데드락을 모니터링하는 스레드

