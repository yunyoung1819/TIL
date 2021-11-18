## :pushpin: EMS Framework
 

### POLESTAR EMS7 SW 아키텍처 설계 목표

- 플러그인 아키텍처 방식의 모듈형 통합 프레임워크 개발 
- 대용량 데이터 처리 기반 프레임워크 NoSQL 기반 (Elastic Search)
- 다국어 지원
- java8, 스프링 프레임워크 사용, Apache Shiro(보안), RESTEasy, hibernate, Quartz, NoSQL 등 오픈소스 라이브러리 사용
- UI는 테페스트리 사용 (테페스트리는 자바 개발자도 어느정도 UI 개발을 할 수 있도록 만든 라이브러리)
- 개발을 진행할 때 클러스터링 구조라는 것을 주의하며 개발 진행


### EMS7 제품 용어 개념

- `AP`: 매니저, 백엔드 서버와 비슷한 개념 (ex: Polestar AP)
- `OMP`: 서버 정보를 수집하기 위해 nkia 자체 개발한 통신 프로토콜. TCP 통신 인터페이스와 비슷
- `License Manager`: 100대의 서버 사용 가능한 라이센스가 등록되어 있으면 더 추가 안되도록 라이센스를 관리하는 매니저
- `Notification Service`: 통보 서비스
- `Resource`: 성능이나 구성 정보를 수집하고 트리에서 조회되는 가장 기본적인 단위
- `measurement`: 성능을 수집
- `Availability`: 가용성. 해당 장비가 정상적인지 아닌지 판별하게 해준다. 리소스나 도메인마다 가용성 판단 정책이 다름
- `Alarm`: 임계치(수치나 문자)를 걸어서 해당 조건에 만족하는 것들을 알람으로 사용자에게 인지시켜주는 알람 서비스
- `Event`: 이벤트
- `Topology Map`: 장비 등의 연관 관계를 도식화해서 보여주는 서비스
- `MeasurementDefinition`: 성능 정보
- `Resource Type`: 리소스 타입
- `Facet`: 구현 명세
- `플랫폼 리소스`: 서버, 네트워크, ICMP 등 Box 형태로 되어있는 것
- `서비스 리소스`: 오라클과 같이 서버에서 기동하는 것
- `컴포넌트 리소스`: CPU, Memory 등은 컴포넌트
- 가장 상위가 리소스이고 `플랫폼 리소스`/`서비스 리소스` (부모/자식 간의 관계를 정의하려고 만듬)
- `연결정보`: 리소스를 등록할 때 필요한 정보


### Facet
- 스케쥴은 `Quartz`로 관리
- 이벤트 수신은 `Trap`, `Syslog`로 처리
- Core 쪽은 하이버네이트 2차 캐시를 사용함
  
  | 지표 | 데이터 형식 |
  | -------| ------- |
  | metric | 숫자 형식 |
  | trait  | 문자 형식 |
  | tabula | 리스트, 테이블 형식 |

- unit: 단위
- getMeasurement: measurement 데이터를 수집하는 메소드
- configurationFacet: 구성정보 (ex: 모델명 등)를 수집해야 하는 경우 구현해야 하는 facet
- RealtimeAdjustmentFacet: 실시간 수집을 지원하는 경우
- EventFacet: 이벤트를 수집해야 하는 경우 구현해야 하는 facet
- AvailableFacet: 해당 facet을 구현하면 가용성 탭이 생김

### 소스 구조

- cygnus가 최상단
- dialect: db별로 특화된 것
- domain: entity
- cygnus-core -> cygnusCoreConfiguration
- cygnus-launcher: 기동을 담당하는 플러그인이 있음
- cygnus-management: measurement, 알람, 통보, dependency: 연관정보
- 그룹 > 플랫폼 리소스 (ex: 서버 등) > 서비스 리소스 (ex: oracle 11g 등) > 컴포넌트 (ex: cpu 등)
- provider는 ResourceProvider를 구현해야함
- providerKey: 리소스 타입 (ex: netwrok.nmsnode, server.cpu)
- icon 확인
    - https://xxx.xxx.xxx.cygnus/cygnus/icon
    
- 모든 ResourceDefinition은 Build 패턴을 사용

```
@Override
public ResourceDefinition getResourceDefinition() {
    return ResourceDefinition.build();
}

addParentResource(MonitorGroupProvider.providerKey): 이 리소스 (ex: 로그모니터 등) 모니터링 그룹 하위에만 등록됨
```


### EMS 주요 테이블 정보

- CMM_RESOURCE: 리소스 테이블
- RESOURCE_CONF_ID: 구성정보 아이디
- CMM_MEASUREMENT
- CORE_CONFIG_PROP: 구성정보, 연결정보

