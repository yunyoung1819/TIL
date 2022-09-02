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

- 이때는 어쩔 수 없이 DOM에 직접적으로 접근해야 하는데, 바로 ref를 사용한다.

> <input ref={(ref) => {this.input=ref}}></input>


### 컴포넌트에 ref 달기

- 리액트에서는 컴포넌트에도 ref를 달 수 있다. 이 방법은 주로 컴포넌트 내부에 있는 DOM을 컴포넌트 외부에서 사용할 때 쓴다.

> <MyComponent
        ref={(ref) => {this.myComponent=ref}}
  />
  
- 이렇게 하면 MyComponent 내부의 메서드 및 멤버 변수에도 접근할 수 있다. 
- 즉 내부의 ref에도 접근할 수 있다. (ex: myComponent.handleClick, myComponent.input 등)


### ES6의 비구조화 할당 문법

- 비구조화 할당 문법은 객체에서 특정 값을 추출하여 따로 레퍼런스를 만들때 유용하다.

```
const object = {
    foo: 1,
    bar: 2
};

const { foo, bar } = object;
console.log(foo, bar);  // 1 2
```

- 이런 문법은 함수의 파라미터를 설정할 때도 동일하게 적용할 수 있다.

```
const object = {
    foo: 1,
    bar: 2
};

funtion print({foo, bar}) {
    console.log(foo, bar)
}

print(object);  // 1 2
```

- 비구조화 할당 문법은 리액트 컴포넌트에서 state 나 props를 참조할 때 자주 사용한다.
- 주로 코드의 가독성과 편리함 때문에 사용하며, 무조건 사용해야 하지는 않는다.

- 예를 들어 아래 render 함수가 있다고 가정하자.

```
render() {
    return (
        <div>
            <div>{this.props.name}</div>
            <div>{this.props.number}</div>
        </div>
    )
}
```

- props를 참조할 때마다 this.props를 반복해서 입력해야 한다는 점이 귀찮다. 
- 이때 비구조화 할당 문법을 사용하면 아래와 같이 작성할 수 있다.

```
render() {
    const { name, number } = this.props;
    return (
        <div>
            <div>{name}</div>
            <div>{number}</div>
        </div>
    )
}
```


### 요약

- 컴포넌트 내부에서 DOM에 직접 접근해야 할 때는 ref를 사용한다.
- 컴포넌트끼리 데이터를 교류할 때는 언제나 데이터를 부모 <-> 자식 흐름으로 교류해야 한다.