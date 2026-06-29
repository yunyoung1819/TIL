## :pushpin: 업무 순삭의 비밀 Agentic AI
###  Claude MCP 데스크톱에서 AI 불러오기

#### Claude MCP
- 클로드 데스크톱 앱 (Claude Desktop App)
- MCP 기술 활용
- AI에게 내 PC 로컬 파일 관리 맡기기

#### MCP
- MCP: Model Context Protocol
- AI를 위한 USB 포트와 같은 역할을 담당

#### Claude
- MCP는 전체 접근을 허용하지 않음
- 사용자가 명시적으로 허용한 범위만 접근 가능
- MCP 기반 AI의 작동 환경 '격리된 공간(Sandbox)'

#### 실습
- 클로드 데스크톱 앱을 통해 파일 옮기고 정리하기
- Canva로 회사 로고 생성하기

#### MCP
- 연결된 커넥터들이 활용 가능한 MCP
- Claude Desktop App 안에서 다양한 외부 도구를 연결하여 작업 범위 확장 가능

#### 커넥터와 MCP 차이
- MCP와 커넥터는 기본적으로 동일한 것으로 봐도 무관함
- 단 구조적으로 커넥터는 MCP를 기반으로 구현된 상위 개념임
- 커넥터의 장점: Claude를 운영하는 Anthropic 기업이 검증한 서비스임
- 간편하게 설정할 수 있고 별도의 코딩없이 사용 설정 가능함
- 커넥터의 단점
  - Claude Pro / Max / Team / Enterprise 버전에서만 사용 가능
  - 커넥터 사용이 불가한 경우 별도의 MCP를 직접 집어넣는 방식으로는 가능