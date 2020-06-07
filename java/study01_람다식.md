# :book: Java Study

## :pushpin: 람다식

### 람다식 (Lambda expression)

- 람다식은 메서드를 하나의 식(expression)으로 표현한 것
- 메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로, 람다식을 익명함수라고도 한다.
- 모든 메서드는 클래스에 포함되어야 하므로 클래스도 새로 만들어야하고, 객체도 생성해야만 비로소 이 메서드를 호출할 수 있다.
- 그러나 람다식은 이 모든 과정없이 람다식 자체만으로도 이 메서드의 역할을 대신할 수 있음
- 람다식은 메서드의 매개변수로 전달되어지는 것이 가능하고, 메서드의 결과로 반환될 수도 있음

````
int[] arr = new int[5];
Arrays.setAll(arr, (i) -> (int)(Math.random()*5)+1);
````

```
int method() {
    return (int) (Math.random()*5) + 1;
}
```

### 람다식 만들기

- 람다식은 '익명함수'답게 메서드에서 이름과 반환타입을 제거하고 매개변수 선언부와 몸통 {} 사이에 ->를 추가

````
반환타입 메서드이름 (매개변수 선언) {
    문장들
}
````


```
(매개변수 선언) -> {
    문장들
}

```


### 메서드를 람다식으로 변환하기

- 메서드 
```
int max(int a, int b) {
    return a > b ? a : b;
}
```

- 람다식 

````
(a, b) -> a > b ? a : b
````

- 메서드 
````
void printVar(String name, int i) {
    System.out.println(name+"="+i);
}
````

- 람다식
````
(name, i) -> System.out.println(name+"="+i)
````

- 메서드
````
int square(int x) {
    return x * x;
}
````

- 람다식 

```
x -> x * x
```

- 메서드

````
int roll() {
    return (int) (Math.random()*6);
}
````

- 람다식

````
() -> (int) (Math.random()*6)
````

- 메서드

```
int sumArr(int[] arr) {
    int sum = 0;
    for (int i : arr)
        sum += i;
    return sum;
}
```

- 람다식

````
(int[] arr) -> {
    int sum = 0;
    for (int i : arr)
        sum += i;
    return sum;
}
````


### 함수형 인터페이스(Functional Interface)

- 람다식은 익명 클래스의 객체와 동등함

> (int a, int b) -> a > b ? a : b


```
new Object() {
    int max(int a, int b) {
        return a > b ? a : b;
    }
}
```

- 람다식을 다루기 위한 인터페이스를 '함수형 인터페이스(functional interface)'라고 부른다.

````
@FunctionalInterface
interface MyFunction {
    public abstract int max(int a, int b)
}
````

- 단, 함수형 인터페이스에는 오직 하나의 추상 메서드만 정의되어 있어야함
- 그래야 람다식과 인터페이스의 메서드가 1:1로 연결될 수 있기 때문 

- 기존
````
List<String> list = Arrays.asList("abc", "aaa", "bbb", "ddd", "aaa");
		
Collections.sort(list, new Comparator<String>() {
    public int compare(String s1, String s2) {
        return s2.compareTo(s1);
        }
	});
````

- 람다식
````
List<String> list = Arrays.asList("abc", "aaa", "bbb", "ddd", "aaa");
Collections.sort(list, (s1, s2) -> s2.compareTo(s1));
````


### 람다식의 타입과 형변환

- 함수형 인터페이스로 람다식을 참조할 수 있지만 람다식의 타입이 함수형 인터페이스의 타입과 일치하는 것은 아님
- 람다식은 익명 객체이고 익명 객체는 타입이 없음
- 아래처럼 대입 연산자의 양변 타입을 일치시키기위해 형 변환이 필요

> MyFunction f = (MyFunction) (() -> {});

- 람다식은 MyFunction 인터페이스를 직접 구현하지 않았지만, 이 인터페이스를 구현한 클래스의 객체와 완전히 동일하기 때문에 위와 같은 형 변환을 허용함
- 그리고 이 형 변환은 생략 가능

> Object obj = (Object) (() -> {});     // 에러. 함수형 인터페이스로만 형 변환 가능 

- 람다식은 Object 타입으로 형 변환할 수 없음
- 람다식은 오직 함수형 인터페이스로만 형 변환이 가능함
- Object 타입으로 형 변환하려면, 먼저 함수형 인터페이스로 변환

> Object obj = ((Object) (MyFunction) (() -> {})).toString();


### 외부 변수를 참조하는 람다식

- 람다식도 익명 객체, 즉 익명 클래스의 인스턴스이므로 람다식에서 외부에 선언된 변수에 접근하는 규칙은 익명 클래스와 동일하다.
†