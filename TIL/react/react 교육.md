## :pushpin: React 라이브러리 교육


### 1. 리액트로 무엇을 할 수 있는가?

- 리액트 (https://www.reactjs.org)
- facebook open source
- 리액트로 만들어진 페이지들 소개
    - 페이스북, 인스타그램, 업비트 등
- 리액트는 컴포넌트 기반의 뷰 라이브러리
    - A JavaScript library for building user interface
- vue (https://vuejs.org) : the Progressive JavaScript Framework
- AngularJS: google에서 만듬
- 리액트는 자유롭게 자바스크립트로 할 수 있음
- 리액트의 컴포넌트에서는 props를 통해서 속성값을 받을 수 있음
    - 리액트 타입 체크: propTypes
- 리액트는 컴포넌트들을 조합하여 재사용하기 쉽게 만들 수 있음
    
    
### 2. React 확장 프로그램

- chrome 웹스토어 - react dev toll
- electron(일렉트론): javascript, html, css를 이용하여 크로스 플랫폼 데스크탑 앱을 만들 수 있음
- 일렉트론으로 만들어진 앱들: skype, insomnia, discord
- Atom 에디터를 만들기 위해서 일렉트론이 탄생


### 3. 우리 회사에는 어떤 제품에 리액트가 쓰이고 있을까?

- Aggrid
- WIZARD
- e-charts (https://echarts.apache.org)


### 4. 환경 준비

- git, node, 에디터(webstorm) 설치


### 5. 리액트 주요 개념

- package.json: 설정 파일
- eslint: 코딩 컨벤션 체크해주는 것 (.eslintrc.js)
- axios: jqueryDML Ajax나 fetch 같은 것. 브라우저 호출용
- Context: 글로벌 변수와 비슷한 개념
- localStorage: 내 브라우저에 저장됨
    - 내 앱에만 데이터가 있어도 되는 경우 로컬 스토리지를 사용함. 로컬 스토리지를 이용하면 서버가 꼭 필요한 로직은 들어갈 수 없음
    - 쿠키와 비슷한 개념
    
    
### 6. atomic design

- 일종의 패턴
- ATOMS --> MOLECULES --> ORGANISMS --> TEMPLATES --> PAGES
- components
    - atoms
    - molecules
    - pages
    
     
### 7. 리덕스 (Redux)

- 플럭스(flux) 패턴에서 비롯
- redux flox

```
ACTION(액션을 일으키는 행위는 디스패치) -> REDUCER(함수, 상태를 변경하고 새로운 상태를 반환) -> STORE(변경된 상태가 스토어에 저장됨)
-> UI (UI는 스토어를 구독하고 있어야함)
```
- STRUCTURE
    - 스토어
    - 액션 & 액션 생성자
    - 리듀서
    
- BEHAVIOR
    - dispatch
    - getState
    - subscribe (변경 사항을 구독하는 것)