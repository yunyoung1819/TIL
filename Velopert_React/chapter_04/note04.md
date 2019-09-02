## 4장. 이벤트 핸들링

### 이벤트

> 이벤트(event): 유저가 웹 브라우저에서 DOM 요소들과 상호 작용하는 것

- 예를 들어 버튼에 마우스 커서를 올렸을 때는 onmouseover 이벤트를 실행하고, 클릭했을 때는 onclick 이벤트를 실행한다.
- Form 요소는 값이 바뀔 때 onchange 이벤트를 실행한다.

### 이벤트를 사용할 때 주의 사항

1) 이벤트 이름은 camelCase로 작성한다.
    - 예를 들어 HTML의 onclick은 리액트에서는 onClick으로 작성한다. 또 onkeyup은 onKeyUp으로 작성한다.
    
2) 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달한다. 
    - HTML에서 이벤트를 설정할 때는 큰따옴표 안에 실행할 코드를 넣었지만, 리액트에서는 함수 형태의 객체를 전달한다.
    
3) DOM 요소에만 이벤트를 설정할 수 있다.
    - div, button, input, form, span 등 DOM 요소에는 이벤트를 설정할 수 있지만, 직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다. 
    - 하지만 전달받은 props를 컴포넌트 내부의 DOM 이벤트로 설정할 수는 있다. 
    
### 이벤트 종류

- 리액트에서 지원하는 이벤트 종류

    - Clipboard
    - Form
    - Composition
    - Mouse
    - Keyboard
    - Selection
    - Focus
    - Touch
    - UI
    - Image
    - Wheel
    - Animation
    - Media
    - Transition
    
### 리액트 이벤트

- 리액트에서 이벤트를 다루는 것은 순수 자바스크립트 또는 jQuery를 사용한 웹 애플리케이션에서 이벤트를 다루는 것과 비슷하다.
- 리액트의 장점 중 하나는 자바스크립트에 익숙하다면 쉽게 활용할 수 있다는 점이다. 
- 기존의 HTML DOM Event를 알면 리액트 컴포넌트의 이벤트도 쉽게 활용할 수 있다.