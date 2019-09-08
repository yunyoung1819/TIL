## 7장. 컴포넌트의 라이프사이클 메서드


### 라이프사이클

- 모든 리액트 컴포넌트에는 라이프사이클(LifeCycle)(수명 주기)이 존재한다.
- Will 접두사가 붙은 메서드는 어떤 작업을 작동하기 전에 실행되는 메서드
- Did 접두사가 붙은 메서드는 어떤 작업을 작동한 후에 실행되는 메서드

- 라이프사이클은 총 세 가지, 즉 마운트, 업데이트, 언마운트 카테고리로 나눈다.


### 컴포넌트의 라이프사이클

- 마운트: 페이지에 컴포넌트가 나타남
- 업데이트: 컴포넌트 정보를 업데이트(리렌더링)
- 언마운트: 페이지에서 컴포넌트가 사라짐 


### 마운트

- DOM이 생성되고 웹 브라우저 상에 나타나는 것을 마운트(mount)라고 한다.
- 이때 호출하는 메서드는 아래와 같다.

    - constructor: 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드
    - getDerivedStateFromProps: props에 있는 값을 state에 동기화하는 메서드
    - render: 우리가 준비한 UI를 렌더링하는 메서드
    - componentDidMount: 컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드
    
    
### 업데이트

- 컴포넌트를 업데이트할 때는 다음 총 네 가지 경우이다.

    1. props가 바뀔 때
    2. state가 바뀔 때
    3. 부모 컴포넌트가 리렌더링될 때
    4. this.forceUpdate로 강제로 렌더링을 트리거할 때
    
- 컴포넌트를 업데이트할 때는 아래 메서드를 호출한다.

    - getDerivedStateFromProps: 이 메서드는 마운트 과정에서도 호출하며, props가 바뀌어서 업데이트할 때도 호출한다.
    - shouldComponentUpdate: 컴포넌트가 리렌더링을 해야할지 말아야할지를 결정하는 메서드이다. 여기서 false를 반환하면 아래 메서드들을 호출하지 않는다.
    - render: 컴포넌트를 리렌더링한다.
    - getSnapshotBeforeUpdate: 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드.
    - componentDidUpdate: 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드.
    

### 언마운트

- 마운트의 반대 과정, 컴포넌트를 DOM에서 제거하는 것을 언마운트(unmount)라고 한다.

    - componentWillUnmount: 컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드.
    
    
### render() 함수

```
render() { ... }
```

- 이 메서드는 컴포넌트 모양새를 정의합니다.


### constructor 메서드

```
constructor(props) { ... }
```

- 컴포넌트의 생성자 메서드
- 컴포넌트를 만들때 처음으로 실행된다.
- 이 메서드에서는 초기 state를 정할 수 있다.


### getDerivedStateFromProps 메서드

```
static getDerivedStateFromProps(nextProps, prevState) {
    if (nextProps.value !== prevState.value) {
        return { value: nextProps.value };
    }
    return null;
}
```
    
- props로 받아온 값을 state에 동기화시키는 용도로 사용
- 컴포넌트를 마운트하거나 props를 변경할 때 호출한다.


### componentDidMount 메서드

```
componentDidMount() { ... }
```

- 이것은 컴포넌트를 만들고, 첫 렌더링을 다 마친 후에 실행한다.
- 이 안에서 다른 자바스크립트 라이브러리 또는 프레임워크의 함수를 호출하거나 이벤트 등록, setTimeout,
setInterval, 네트워크 요청 같은 비동기 작업을 처리한다.


### shouldComponentUpdate 메서드

```
shouldComponentUpdate(nextProps, nextState) { ... }
```

- 이것은 props 또는 state를 변경했을 때, 리렌더링을 시작할지 여부를 지정하는 메서드이다.
- 이 메서드에서는 반드시 true 값 또는 false 값을 반환해야 한다.
- 프로젝트 성능을 최적화할 때, 상황에 맞는 알고리즘을 작성하여 리렌더링을 방지할 때는 false 값을 반한하게 한다.


### getSnapshotBeforeUpdate 메서드

- 이 메서드는 render 메서드를 호출한 후 DOM에 변화를 반영하기 바로 직전에 호출하는 메서드
- 주로 업데이트하기 직전의 값을 참고할 일이 있을 때 활용된다. (ex: 스크롤바 위치)

```
getSnapshotBeforeUpdate(prevProps, prevState) {
    if (prevState.array !== this.state.array) {
        const { scrollTop, scrollHeight } = this.list
        return { scrollTop, scrollHeight };
    }
}
```


### componentDidUpdate 메서드

```
componentDidUpdate(prevProps, prevState, snapshot) { ... }
```

- 이것은 리렌더링을 완료한 후 실행한다.
- 업데이트가 끝난 직후이므로, DOM 관련 처리를 해도 무방하다.
- 여기에서는 prevProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근할 수 있다.


### componentWillUnmount 메서드

```
componentWillUnmount() { ... }
```

- 이것은 컴포넌트를 DOM에서 제거할 때 실행한다.
- componentDidMount에서 등록한 이벤트, 타이머,직접 생성한 DOM이 있다면 여기에서 제거 작업을 해야 한다.