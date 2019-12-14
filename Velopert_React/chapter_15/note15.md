## 15장. 리덕스 미들웨어와 외부 데이터 연동


### 미들웨어 이해

- 리덕스 미들웨어(middleware)는 액션을 디스패치했을 때 리듀서에서 이를 처리하기 전에 사전에 지정된 작업들을 실행
- 액션과 리듀서 사이의 중간자

### 비동기 작업을 처리하는 미들웨어 사용

- reudx-thunk
- redux-promise-middleware
- redux-pender

### redux-thunk

- 리덕스를 사용하는 애플리케이션에서 비동기 작업을 처리할 때 가장 기본적인 방법은 redux-thunk 미들웨어를 사용하는 것이다.
- thunk는 특정 작업을 나중에 할 수 있도록 미루려고 함수 형태로 감싼 것을 의미함

### Promise

- Promise는 ES6 문법에서 비동기 처리를 다루는데 사용하는 객체
- Promise는 값을 리턴하거나 오류를 발생시킬 수도 있다.
- Promise에서 결과값을 반환할 때는 resolve(결과 값)을 작성하고, 오류를 발생시킬 때는 reject(오류)를 작성
- 반환하는 결과 값과 오류는 .then 또는 .catch에 전달하는 함수의 파라미터로 설정 

### axios

- Promise 기반 HTTP 클라이언트 라이브러리이다. 
- axios로 웹 요청을 했을 때 반한되는 객체는 해당 요청의 응답 정보를 지닌 객체


### 오청 완료 후나 오류가 발생했을 때 추가할 작업

- redux-thunk로 만든 액션 함수는 Promise를 반환하기 때문에 해당 함수를 호출하고는 뒤에 .then 또는 .catch를 입력해서 구현하면 된다.
- create-react-app 으로 만든 프로젝트는 바벨 설정에 Async to generator transform 플러그인이 적용되어 
- async/await 라는 ES7 문법을 사용할 수 있다.
- async/await을 사용할 때는 await를 쓸 함수의 앞부분에 async 키워드를 붙여주고, 기다려야할 Promise 앞에
- await 키워드를 붙여주면 된다.
- await를 사용할 때는 꼭 try~catch 문으로 오류를 처리해야한다.
- 오류를 처리하지 않는다면, 오류가 발생했을 때 해당 함수는 오류 위치에서 작업을 중지하고 더 이상 진행하지 않음.


### 리덕스에서 비동기 웹 요청

- 리덕스에서 비동기 작업을 처리하는 방법은 redux-thunk 외에도 여러 가지가 있다.
- redux-promise-middleware, reudx-saga, redux-pender, redux-observable 등이 있다.


### redux-pender

- redux-pender는 Promise 기반 액션들을 관리하는 미들웨어가 포함되어 있는 라이브러리