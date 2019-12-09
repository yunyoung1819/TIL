## 14장. 리덕스, 더 편하게 사용


### Immutable.js 익히기

- Immutable.js는 자바스크립트에서 불변성 데이터를 다룰 수 있도록 도와준다.

### Map

- Immutable의 Map은 객체 대신 사용하는 데이터 구조
- 자바스크립트에 내장된 Map과는 다름

```
const { Map } = Immutable;

const data = Map({
    a: 1,
    b: 2
});
```

- Map을 사용할 때는 Map 함수 안에 객체를 넣어서 호출 
```
const { Map } = Immutable;

const data = Map({
    a: 1,
    b: 2,
    c: Map({
        d: 3,
        e: 4,
        f: 5
    })
})
```


### List

- List는 Immutable 데이터 구조로 배열 대신 사용
- 배열과 동일하게 map, filter, sort, push, pop 함수를 내장하고 있다.
- 이 내장함수를 실행하면 List 자체를 변경하는 것이 아니라 새로운 List를 반환한다는 것에 주의

```
const { List } = Immutable;

const list = List([0,1,2,3,4]);
```


### Ducks 파일 구조

- 리덕스에서 사용하는 파일들은 일반적으로 액션 타입, 액션 생성 함수, 리듀서 이렇게 세 종류로 분리하여 관리한다.
- 액션 타입, 액션 생성 함수, 리듀서를 모두 한 파일에서 모듈화하여 관리하면 어떨까? 라는 아이디어로 만든 파일 구조가
바로 Ducks 파일 구조이다.


### redux-actions를 이용한 더 쉬운 액션 관리

- redux-actions 패키지에는 리덕스 액션들을 관리할 때 유용한 createAction과 handleAction 함수가 있다.

```
$ yarn add redux-actions
```

```
import { createAction, handleActions } from 'redux-actions';
```

- createAction 함수는 액션 생성 함수를 간단하게 만들어준다.
- switch 문 대신 handleActions tkdyd 
- bindActionCreators : 이 함수의 첫번째 파라미터는 액션 생성 함수들이 들어 있는 객체고, 두번째 파라미터는 dispatch 이다.
