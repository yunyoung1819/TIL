# :book: 객체지향 프로그래밍

## :pushpin: 내부 클래스, 람다식, 스트림

### 람다식 (Lambda Expression)

- 자바에서 함수형 프로그래밍(functional programming)을 구현하는 방식
- 클래스를 생성하지 않고 함수의 호출만으로 기능을 수행
- 함수형 인터페이스를 선언함
- 자바 8부터 지원되는 기능 


### 함수형 프로그래밍이란?

- 순수 함수(pure function)를 구현하고 호출
- 매개 변수먼을 사용하도록 만든 함수로 외부 자료에 부수적인 영향(side effect)가 발생하지 않도록 함
- 입력 받은 자료를 기반으로 수행되고 외부에 영향을 미치지 않으므로 병렬처리 등에 가능 
- 안정적인 확장성 있는 프로그래밍 방식


### 람다식 문법

- 매개변수 하나인 경우 괄호 생략 가능 (두개인 경우는 괄호를 생략할 수 없음)

````
str -> {System.out.println(str);}
````

- 중괄호 안의 구현부가 한 문장인 경우 중괄호 생략

```
str -> System.out.println(str);
```

- 중괄호 안의 구현부가 한 문장이라도 return문은 중괄호를 생략할 수 없음

```
str -> return str.length();   // 오류
```

- 중괄호 안의 구현부가 반환문 하나라면 return과 중괄호를 모두 생략할 수 있음

````
(x,y) -> x + y    // 두 값을 더하여 반환
````

```
str -> str.length() // 문자열 길이를 반환 
```


### 함수를 변수처럼 사용하는 람다식

- 프로그램에서 변수는...
    - 자료형에 기반하여 선언하고 int a;
    - 매개변수로 전달하고 int add(int x, int y);
    - 메서드의 반환 값으로 사용 return num;
    
- 람다식은 프로그램 내에서 변수처럼 사용할 수 있음 



### 스트림(Stream)

- 자료의 대상과 관계없이 동일한 연산을 수행할 수 있는 기능(자료의 추상화)
- 배열, 컬렉션에 동일한 연산이 수행되어 일관성 있는 처리 가능
- 한번 생성하고 사용한 스트림은 재사용할 수 없음
- 스트림 연산은 기존 자료를 변경하지 않음
- 중간 연산과 최종 연산으로 구분됨
- 최종 연산이 수행되어야 모든 연산이 적용되는 지연 연산 


### 스트림 연산 - 중간 연산

- 중간 연산 - filter(), map()
- 조건에 맞는 요소를 추출(filter()) 하거나 요소를 변환 함 (map())

> 문자열의 길이가 5이상인 요소만 출력하기

````
sList.stream().filter(s -> s.length() >= 5).forEach(s -> System.out.println(s));
````

> 고객 클래스에서 고객 이름만 가져오기

````
customerList.stream().map(c -> c.getName()).forEach(s -> System.out.println(s));
````


### 스트림 연산 - 최종 연산

- 스트림의 자료를 소모하면서 연산을 수행
- 최종 연산 후에 스트림은 더 이상 다른 연산을 적용할 수 없음
    - forEach(): 요소를 하나씩 꺼내 옴
    - count: 요소의 개수
    - sum: 요소의 합
- 이 외도 여러가지 최종 연산이 있음


### reduce() 연산

- 정의된 연산이 아닌 프로그래머가 직접 지정하는 연산을 적용
- 최종 연산으로 스트림의 요소를 소모하며 연산 수행
- 배열의 모든 요소의 합을 구하는 reduce() 연산

````
Arrays.stream(arr).reduce(0, (a,b) -> a + b));
````

- 두 번째 요소로 전달되는 람다식에 따라 다양한 기능을 수행 

```
public class ReduceTest {
	
	public static void main(String[] args) {
		
		String[] greetings = {"안녕하세요~~~", "hello", "Good morning", "반갑습ㄴ디"};
		
		System.out.println(Arrays.stream(greetings).reduce("", (s1, s2) -> {
			if (s1.getBytes().length >= s2.getBytes().length)
				return s1;
			else return s2;
		}));
	}
	
}

```

- BinaryOperator로 구현하기 

```
import java.util.Arrays;
import java.util.function.BinaryOperator;

class CompareString implements BinaryOperator<String> {

	@Override
	public String apply(String s1, String s2) {
		if (s1.getBytes().length >= s2.getBytes().length)
			return s1;
		else return s2;
	}
	
}

public class ReduceTest {
	
	public static void main(String[] args) {
		
		String[] greetings = {"안녕하세요~~~", "hello", "Good morning", "반갑습ㄴ디"};
		
		System.out.println(Arrays.stream(greetings).reduce("", (s1, s2) -> {
			if (s1.getBytes().length >= s2.getBytes().length)
				return s1;
			else return s2;
		}));
		
		System.out.println(Arrays.stream(greetings).reduce(new CompareString()).get());
	}
	
}

```