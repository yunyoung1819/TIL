# pushpin: Spring Boot JWT Tutorial
## :seedling: 1. JWT 소개, 프로젝트 생성

### JWT
- RFC 7519 웹 표준으로 지정
- JSON 객체를 사용해서 토큰 자체에 정보들을 저장하고 있는 Web Token이라고 정의할 수 있음
- jWT는 `Header`, `Payload`, `Signature` 3개 부분으로 구성되어 있음
  - Header: Signature를 해싱하기 위한 알고리즘 정보들이 담겨있음
  - 