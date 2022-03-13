## 8장. 함수형 컴포넌트

### 함수형 컴포넌트 사용법

- 리액트에서 컴포넌트는 지금까지 해온 것처럼 class 문법을 사용하여 정의한다.
- 컴포넌트에서 라이프사이클 API나 state를 사용해야할 때는 꼭 아래 형식으로 정의해야 한다,

```
import React, { Component } from 'react';

class Hello extends React.Component {
    render() {
        return (
            <div>Hello {this.props.name}</div>
        );
    }
}

export default Hello;
```

- 컴포넌트를 만들 때마다 클래스를 만들고, 또 그 안에 render 메서드를 만드는 것이 번거롭다.
- 만들어야할 컴포넌트가 라이프사이클 API와 state를 사용할 필요가 없고, 오로지 props를 전달받아 뷰를 렌더링하는 역할만 한다면 컴포넌트를 더 간단하게 선언할 수 있다.


### 함수형 컴포넌트 사용법

- 아래와 같이 순수 함수만으로도 컴포넌트를 선언할 수 있다.

```
import React from 'react';

function Hello(props) {
    return (
        <div>Hello {props.name} </div>
    )
}

export default Hello;
```

- ES6의 화살표 함수와 비구조화 할당 문법을 사용하면 아래와 같이 컴포넌트를 선언할 수도 있다.

```
import React from 'react';

const Hello = ({name}) => {
    return (
        <div>Hello {name} </div>
    }
}

export default Hello;
```

- 또는 이런 식으로 {}를 생략할 수도 있다.

```
import React from 'react';

const Hello = ({name}) => (
    <div> Hello {name} </div>
)

```


### 언제 함수형 컴포넌트를 사용해야 할까?

- 함수형 컴포넌트는 컴포넌트에서 라이프사이클, state 등 불필요한 기능을 제거한 상태이기 때문에 메모리 소모량은 일반 클래스형 컴포넌트보다 적다.
- 리액트 v16 이상에서는 함수형 컴포넌트 성능이 클래스형 컴포넌트보다 조금 빠르다.

- 리액트 프로젝트에서는 state를 사용하는 컴포넌트 개수를 최소화하면 좋다.
- 따라서 컴포넌트를 만들 때는 대부분 함수형으로 작성하여 state를 사용하는 컴포넌트 개수를 줄이는 방향으로 향한다.
- state나 라이프사이클 API를 꼭 써야 할 때만 클래스 형태로 변환하여 컴포넌트를 작성한다. 