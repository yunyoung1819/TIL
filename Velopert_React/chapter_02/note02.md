## 2장. JSX


#### 코드 이해

```
import React, { Component } from 'react';
```

- Node.js 의 주요 특징은 코드를 모듈화하여 재사용할 수 있다는 점이다.
- 이렇게 모듈들을 js 파일에서 불러와 사용할 수 있는데, 이때 사용하는 코드는 아래와 같다.

```
var fs = require('fs');
```

- ES6 (ECMAScript6) 에서는 모듈을 불러오는 새로운 키워드가 생겼다. 바로 import 이다.
- import를 키워드를 사용하여 모듈을 불러오는 방법은 아래와 같다.

```
import fs from 'fs';
```

- 위 코드는 아래 이전 자바스크립트 문법과 동일하다.

```
var React = require('react');
var Component = React.Component;
```

- 이렇게 파일을 모듈화해서 사용하는 것은 Node.js의 기능이다.
- 웹 브라우저에서 사용하는 자바스크립트는 Node.js 런타임으로 실행하는 것이 아니기 때문에 자체적으로 이 기능을 지원하지 않는다.

- 하지만 이런 특징을 웹 브라우저에서도 비슷하게 사용할 수 있는 방법이 바로 번들링(bundling) 도구를 이용하는 것이다.
- 여기서 번들(bundle)은 '묶는다'는 뜻으로 파일들을 묶듯이 연결하는 것이다.
- 번들링 도구로는 Browserify, RequireJS, webpack 등이 대표적이다.
- 이런 번들링 도구를 사용하면, require (또는 import)로 모듈을 불러왔을 때 번들링되면서 모듈들을 파일 하나로 합쳐준다.
- 이렇게 파일들을 불러오는 것은 webpack의 로더(loader)가 담당한다.
- babel-loader는 js 파일들을 불러오면서 ES6로 작성된 코드를 ES5 문법으로 변환해준다.

```
class App extends Component
```

- 위 코드는 App이라는 클래스를 선언한다.
- 이 클래스는 리액트 라이브러리 내부에 있는 Component 클래스를 상속한다. 

> ES6의 클래스(class) 문법

```
class Dog {
    constructor(name) {
        this.name = name;
    }
    say() {
        console.log(this.name + ': 멍멍');
    }
}

const dog = new Dog('흰둥이');
dog.say();
```

- render() 함수 : 이 함수 내부에서는 컴포넌트를 유저에게 어떻게 보일지 return 한다.


#### JSX

- JSX: 자바스크립트의 확장 문법으로 XML과 매우 비슷하게 생겼다.
- 이런 형식으로 작성한 코드는 나중에 코드가 번들링되면서 bable-loader를 사용하여 자바스크립트로 변환된다.