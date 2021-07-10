# :book: 엘라스틱서치 쿡북

###### 엘라스틱서치 쿡북을 읽고 그 내용을 요약한 글 입니다. 상세 내용은 책을 참조해주세요.

---------------------------------------------------------------------------

## :pushpin: 1장. 시작하기

### 노드와 클러스터 이해

- 모든 일래스틱서치 인스턴스는 노드이다.
- 여러 노드는 클러스터로 그룹 짓는다. 
- 기본 노드에 데이터를 저장하고 요청과 응답을 처리한다.
- 다중 노드가 있는 클러스터에서 마스터 노드가 죽으면 마스터 자격이 있는 노드를 새로운 마스터로 선출한다. 
이 접근 방법으로 장애 조치(failover)를 자동으로 하도록 일래스틱서치 클러스터를 설정할 수 있다.

### 노드 종류

- 일래스틱서치에는 다음과 같은 네 종류의 노드가 있다.
    - REST: 응답과 검색에 관한 모든 작업을 처리할 수 있는 마스터 노드.
    - 데이터 노드: 데이터를 내부에 저장할 수 있는 노드
    - 수집 노드: 수집 파이프라인을 처리할 수 있는 노드
    - 클라이언트 노드: 어떤 방식이든 무언가 처리하는데 사용하는 노드
    
    
### 노드 서비스 이해

- 노드가 실행 중일 때 인스턴스 자신은 많은 서비스를 관리한다.
    - 클러스터 서비스
    - 색인 서비스
    - 매핑 서비스
    - 네트워크 서비스 (HTTP REST 서비스 기본값: 9200 포트 / 내부 ES 프로토콜: 9300 포트)
    - 플러그인 서비스
    - 집계 서비스
    - 인제스트 서비스
    - 언어 스크립팅 서비스 


### 데이터 관리 

- 주요 데이터 컨테이너를 색인(index)이라 부르는데 이는 전통적인 SQL 세상의 데이터베이스와 비슷하다고 볼 수 있음
- 매핑은 레코드 작성 방법(필드)을 기술한 것
- 기본적으로 스키마가 없는(schema-less) 데이터 저장소이다.
- 일래스틱서치에 저장해야 하는 모든 레코드는 JSON 객체가 돼야 한다.
- 대량의 레코드를 관리하기 위해 색인을 여러 개의 부분(샤드)으로 분할하는 일반적인 방식을 통해 여러 노드로 분산할 수 있음

일래스틱서치 | SQL | MongoDB
-----| ------| ------|
색인 | 데이터베이스 | 데이터베이스
샤드 | 샤드 | 샤드
매핑/타입 | 테이블 | 컬렉션
필드 | 칼럼 | 필드
객체(JSON 객체) | 레코드 (튜플) | 레코드(BSON 객체)


### 클러스터, 복제, 샤딩의 이해

- 색인은 한 개 이상의 레플리카(일래스틱서치가 데이터 전체 사본을 자동으로 관리한다)를 가질 수 있다.
- 데이터 손실을 막고 고가용성을 위해 최소한 한 개의 레플리카를 갖는 것이 좋다.


### 클러스터 상태 표시기

- 그린(Green): 이 상태는 모든 것이 정상임을 나타낸다.
- 엘로(Yello): 이 상태는 일부 샤드가 누락됐으나 동작은 하고 있음을 나타낸다.
- 레드(Red): 일부 기본 샤드가 누락됐다. 클러스터에 쓰기를 허용하지 않는다. 에러가 발생하며, 누락된 샤드 때문에 작업은 제대로 처리되지 않는다. 누락된 샤드를 복구할 수 없다면 데이터 손실이 생긴다.

### 옐로 상태 해소

- 대부분 옐로 (Yello) 상태는 할당되지 않은 일부 샤드 때문이다.
- 클러스터가 '복구(recovery)' 상태에 있다면 샤드 시작 절차가 마칠 때까지 기다리면 된다.
- 복구가 끝난 후에도 클러스터가 여전히 옐로 상태라면 레플리카를 담을 노드가 충분하지 않다고 할 수 있다.
- 이 때는 레플리카 개수를 줄이거나 필요한 노드를 추가하면 된다.

### 레드 상태 해소

- 이 경우 누락된 노드를 복구해야 한다.
- 노드를 재시작하고 시스템이 옐로나 그린 상태로 돌아온다면 다행이다.
- 색인을 삭제하고 백업이나 스냅샷 또는 다른 소스로부터 복구하자.

### 일래스틱서치와 통신

1. HTTP 프로토콜 
2. 네이티브 프로토콜