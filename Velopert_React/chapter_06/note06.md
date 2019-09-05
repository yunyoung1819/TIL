## 6장. 컴포넌트 반복

### 자바스크립트 배열의 map() 함수

- 자바스크립트 배열 객체의 내장 함수인 map 함수를 사용하여 반복되는 컴포넌트를 렌더링할 수 있다.
- map 함수는 파라미터로 전달된 함수를 사용하여 배열 내 각 요소를 프로세싱한 후 그 결과로 새로운 배열을 생성한다..

```
arr.map(callback, [thisArg])
```

- callback: 새로운 배열의 요소를 생성하는 함수로 파라미터는 아래 세가지이다.
    - currentValue: 현재 처리하고 있는 요소
    - index: 현재 처리하고 있는 요소의 index 값
    - array: 현재 처리하고 있는 원본 배열
- thisArg(선택항목): callback 함수 내부에서 사용할 this 레퍼런스

- map 함수는 기존 배열로 새로운 배열을 만드는 역할을 한다. 

```
const numbers = [1,2,3,4,5];
const result = numbers.map(num => num * num);
console.log(result);
```