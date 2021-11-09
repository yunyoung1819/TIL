## 3장. 컴포넌트

#### 컴포넌트

- 리액트를 사용하여 애플리케이션의 인터페이스를 설계할 때 사용자가 볼 수 있는 요소는 여러 가지 컴포넌트로 구성되어 있다. 

#### props

- props는 properties를 줄인 표현으로 컴포넌트 속성을 설정할 때 사용하는 요소이다.
- props 값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서만 설정할 수 있다.

- props값 설정 및 검증

    - props 렌더링하기
    - props 값 설정하기
    - props 기본 값 설정하기
    - props 값 검증하기 
    
- props에 접근할 때는 this 키워드를 사용하여 접근한다.


### props 기본값 설정: defaultProps

- props 값을 지정하지 않았을 때 기본값으로 설정한다.

### props 검증: propTypes

- 컴포넌트의 필수 props를 지정하거나 props 타입(type)을 지정할 때는 propTypes를 사용한다.

### 더 많은 propTypes 종류

- propTypes에서 설정할 수 있는 종류는 여러가지이다.

    - array: 배열
    - bool: 참, 거짓
    - func: 함수
    - number: 숫자
    - object: 객체
    - string: 문자열
    - symbol: ES6 문법의 심벌 개체
    - node: 렌더링할 수 있는 모든 것(숫자, 문자열, element 또는 이들로 구성된 배열)
    - element: 리액트 요소
    - instanceOf(MyClass): 특정 클래스의 인스턴스
    - oneOf(['Male', 'Female']): 주어진 배열 요소 중 값 하나
    - oneOfType([React.PropTypes.string, React.PropTypes.number]): 주어진 배열 안의 종류 중 하나
    - arrayOf(React.PropTypes.number): 주어진 종류로 구성된 배열
    - objectOf(React.PropTypes.number): 주어진 종류의 값을 가진 객체
    - shapge({name: React.PropTypes.string, age: React.PropTypes.number}): 주어진 스키마를 가진 객체
    - any: 아무 종류
    
### state
 
 - props는 부모 컴포넌트가 설정하며, 컴포넌트 자신은 해당 props를 읽기 전용으로만 사용할 수 있다.
 - 반면 컴포넌트 내부에서 읽고 또 업데이트할 수 있는 값을 사용하려면 state를 써야한다.
 - state는 언제나 기본 값을 미리 설정해야 사용할 수 있으며, this.setState() 메서드로만 값을 업데이트해야 한다.
 
 
### 컴포넌트의 생성자 메서드: constructor()
 
 - state 초기값은 컴포넌트의 생성자 메서드인 constructor 내부에서 설정한다. 
 - 생성자 메서드는 컴포넌트를 새로 만들때 실행된다.
 - 우리가 만든 컴포넌트는 리액트의 Component 클래스를 상속한다. 
 - 따로 constructor 메서드를 만들어 주지 않으면 Component 클래스의 생성자 메서드를 그대로 사용한다.
 - 직접 constructor 메서드를 작성하여 생성자 메서드에서 추가 작업을 하려면, 메서드 내부에서 부모 클래스인 Component의 constructor 메서드를 먼저 호출해야 한다.
 - 이때 super 키워드를 사용한다.
 - 컴포넌트를 만들때 props 값들을 사용하므로 props를 메서드의 파라미터로 전달한다. 
 
 
### state 값 업데이트: setState()

- state 값을 업데이트할 때는 this.setState() 메서드를 사용한다.

```
this.setState({
    수정할 필드 이름 : 값,
    수정할 또 다른 필드 이름: 값
});
```

### ES6의 화살표 함수

- 화살표 함수(arrow function)는 ES6 문법에서 함수를 표현하는 새로운 방식이다.
- 그렇다고해서 기존 function을 이용한 함수 선언 방식을 아예 대체하지는 않는다.
- 일반 함수는 자신이 종속된 객체를 this로 가리키며, 화살표 함수는 자신이 종속된 인스턴스를 가리킨다.
- 화살표 함수는 값을 연산하여 바로 반환해야 할 때 사용하면 가독성이 높다. 

```
function twice(value) {
    return value * 2;
}
```

```
const triple = (value) => value * 3;
```

- 위처럼 따로 {}를 열어주지 않으면 연산한 값을 그대로 반환한다는 의미이다. 


### state를 constructor에서 꺼내기

- 원래 초기 state는 constructor 메서드에서 정의해야 하지만, defaultProps와 propTypes를 정의할 때 사용한 transform-class-properties 문법으로 constructor 바깥에서 정의할 수도 있다.

```
class MyComponent extends Component {
    
    static defaultProps = {
        name: '기본 이름'
    }
    
    static propTypes = {
        name: PropTypes.string,
        age: PropTypes.number.isRequired
    }
    
    state = {
        number:0
    }
}
```

### state 값을 업데이트할 때 주의 사항

- state 값을 업데이트할 때는 언제나 .setState로만 업데이트해야 한다.
- setState() 메서드가 하는 역할은 파라미터로 전달받은 필드를 업데이트한 후 컴포넌트가 리렌더링하도록 트리거하는 것이다.
- 하지만 state에 직접 접근하여 값을 수정하면 컴포넌트를 자동으로 리렌더링하지 않는다.

### props vs state

- props와 state는 둘 다 컴포넌트에서 사용하거나 렌더링할 데이터를 담고 있으므로 비슷해보일 수도 있지만, 역할은 매우 다르다.
- props는 부모 컴포넌트가 설정하고, state는 컴포넌트 자체적으로 진니 값으로 컴포넌트 내부에서 값을 업데이트한다. 