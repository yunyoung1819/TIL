## 5장. ref: DOM에 이름달기 


### ref

- 일반 HTML 에서 DOM 요소에 이름을 달 때는 id를 사용한다.

```
<div id="my-element"></div>
```

- HTML에서 id를 사용하여 DOM에 이름을 다는 것처럼 리액트 프로젝트 내부에서 DOM에 이름을 다는 방법이 있다.
- 바로 ref(reference의 줄임) 개념이다.


### ref는 어떤 상황에서 사용할까?

- 특정 DOM에 작업을 해야할 때 ref를 사용한다.
- "DOM을 꼭 직접적으로 건드려야할 때" 사용한다.


### DOM을 꼭 사용해야 하는 상황

1. 특정 input에 포커스 주기
2. 스크롤박스 조작하기
3. Canvas 요소에 그림 그리기 등

- 이떄는 어쩔 수 없이 DOM에 직접적으로 접근해야 하는데, 바로 ref를 사용한다.

> <input ref={(ref) => {this.input=ref}}></input>