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