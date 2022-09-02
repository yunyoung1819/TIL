## 13장. 리덕스로 리액트 애플리케이션 상태 관리


### 작업 환경 설정

- react-redux: 리액트 컴포넌트에서 리덕스를 더욱 간편하게 사용할 수 있게하는 라이브러리
- actions: 액션 타입과 액션 생성자 파일을 저장
- components: 컴포넌트의 뷰가 어떻게 생길지만 담당하는 프리젠테이셔널 컴포넌트를 저장
- containers: 스토어에 있는 상태를 props로 받아오는 컨테이너 컴포넌트들을 저장
- reducers: 스토어의 기본 상태 값과 상태의 업데이트를 담당하는 리듀서 파일들을 저장
- lib: 일부 컴포넌트에서 함께 사용되는 파일을 저장


### 액션

- 액션은 객체이다.
- 모든 액션 객체에는 type 값이 필수로 있어야 한다.


### 액션 생성 함수

- 액션울 만들어내는 함수


### 리듀서

- 리듀서는 액션의 type에 따라 변화를 일으키는 함수
- 리듀서 함수는 state와 action을 파라미터로 가지는 함수며, 그 함수 내부에서 switch문으로 action.type에 따라 상태에 다른 변화를 일으킨다.


### 스토어

- 리덕스에서 가장 핵심적인 인스턴스이다.
- 이 안에 현재 상태가 내장되어 있고, 상태를 업데이트할 때마다 구독 중인 함수들을 호출한다.


### Provider

- Provider는 react-redux 라이브러리에 내장된 리액트 애플리케이션에 손쉽게 스토어를 연동할 수 있도록 도와주는 컴포넌트


### connect 함수

- react-redux 라이브러리의 connect 함수를 사용하여 컴포넌트를 스토어에 연결시킨다.
- connect 함수에는 파라미터가 세 개가 들어간다.

```
connect([mapStateToProps], [mapDispatchToProps], [mergeProps])
```

> - mapStateToProps: store.getState() 결과 값인 state를 파라미터로 받아 컴포넌트의 props로 사용할 객체를 반환
> - mapDispatchToProps: dispatch를 파라미터로 받아 액션을 디스패치하는 함수들을 객체 안에 넣어서 반환
> - mergeProps: state와 dispatch가 동시에 필요한 함수를 props로 전달해야할 때 사용하는데, 일반적으로 잘 사용하지않음
