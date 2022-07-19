# :book: 모든 개발자를 위한 HTTP 웹 기본 지식
## :pushpin: HTTP API 설계 예시

### :seedling: HTTP API 설계 예시
- HTTP API - 컬렉션
  - POST 기반 등록
  - 예) 회원 관리 API 제공
- HTTP API - 스토어
  - PUT 기반 등록
  - 예) 정적 컨텐츠 관리, 원격 파일 관리
- HTML FORM 사용
  - 웹 페이지 회원 관리
  - GET, POST만 지원

### :seedling: 회원 관리 시스템
#### API 설계 - POST 기반 등록

- **회원** 목록 /members -> GET
- **회원** 등록 /members -> POST
- **회원** 조회 /members/{id} -> GET
- **회원** 수정 /members/{id} -> PATCH, PUT, POST (PUT: 덮어쓰기 PATCH: 부분 수정)
- **회원** 삭제 /members/{id} -> DELETE