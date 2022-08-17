# :book: selab-study 

## :pushpin: Topic. Checked Exception VS Unchecked Exception

### 오류(Error)와 예외(Exception)

▶ 예외
- 프로그래밍에서 예외란 입력 값에 대한 처리가 불가능하거나, 프로그램 실행 중에 참조된 값이 잘못된 경우 등 
정상적인 프로그램의 흐름에 어긋나는 경우 
- 예외는 개발자가 직접 처리할 수 있기 때문에 예외 상황을 미리 예측하여 핸들링할 수 있음

▶ 오류
- 시스템에 무엇인가 비정상적인 상황이 발생한 경우
- 주로 자바 가상 머신에서 발생함. 예외와 반대로 이를 애플리케이션 코드에서 잡을 수 없음
- 오류의 예시 (OutOfMemoryError, ThreadDeath, StackOverflowError 등)


### Exception Class 계층

- Exception(예외)는 아래 그림과 같이 Checked Exception과 Unchecked Exception으로 구분할 수 있음
- 즉 RuntimeException을 상속하지 않은 클래스는 Checked Exception, 반대로 상속한 클래스는 Unchecked Exception으로 분류할 수 있음

![](../images/예외.PNG)

### Checked Exception

- 명시적인 예외 처리를 강제하기 때문에 Checked Exception이라고 함
- 반드시 try ~ catch로 예외를 잡거나 throw로 호출한 메소드에게 예외를 던져야 함
- Exception 처리 코드를 compiler가 check
- ex) IOException, ClassNotFoundException 등

### Unchecked Exception

- 배열의 범위를 벗어난다거나(IndexOutOfBoundsException) 값이 null인 참조변수의 멤버를 호출하거나 (NullPointerXception) 
클래스 간의 형 변환을 잘못했다던가 (ClassCastException) 정수를 0으로 나누려 했다거나 (ArithmeticException)하는 경우에 발생하는 예외들
- 컴파일하는데 문제없지만 실행하면 문제가 발생함
- 명시적인 예외 처리를 강제하지 않기 때문에 Unchecked Exception이라고 함
- 명시적인 예외 처리란 try ~ catch로 잡거나 throw로 호출한 메소드에게 예외를 던지지 않는 행위를 말함 
- 등 NullPointerException, ClassCastException 등

|    |Checked Exception|Unchecked Exception|
|----|---|----|
|처리여부|반드시 예외를 처리해야함|명시적인 처리를 강제하지 않음|
|확인시점|컴파일 단계|실행단계
|예외 발생시 트랜잭션 처리|roll-back하지 않음|roll-back함
|대표 예외|Exception을 상속받는 하위 클래스 중 RuntimeException을 제외한 모든 예외(대표적으로 IOException)|RuntimeException 하위 예외 (대표적으로 NullPointerException)



#### 참고 글
- https://joswlv.github.io/2018/10/29/java_exception/
- https://steady-coding.tistory.com/583