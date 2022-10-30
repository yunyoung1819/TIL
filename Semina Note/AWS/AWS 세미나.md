## AWS 세미나 (AWS Community Day 2022)

## :pushpin: AWS Athena

> Amazon Athena는 표준 SQL을 사용해 Amazon S3에 저장된 데이터를 간편하게 분석할 수 있는 대화식 쿼리 서비스
> Athena는 서버리스 서비스이므로 관리할 인프라가 없으며 실행한 쿼리에 대해서만 비용을 지불하면 됨


### Athena란?
- Serverless SQL Query Tool
- Presto(Distributed SQL Query Engine)를 Wrapping해서 만듬
- Data Analytic을 위해 주로 사용, 데이터 탐색에 유리함
- Data 스캔 용량을 기반으로 요금이 청구됨


### 언제 사용?
- S3 기반 Data lake에 있는 데이터를 쿼리할 때
- 인프라, 운영, 애플리케이션 로그를 분석할 때


### Athena 사용법
- AWS Console > Amazon Athena > 쿼리 편집기


### AWS Step Functions
- 개발자가 AWS를 사용하여 분산 애플리케이션을 구축하고 프로세스를 자동화할 수 있음
- 두가지 워크 플로우 지원