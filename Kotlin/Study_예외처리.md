## :pushpin: 코틀린 기초

### 예외 처리
- 코틀린의 모든 예외 클래스는 최상위 예외 클래스인 `Throwable` 을 상속한다.

![](./images/예외처리.png)

- **Error**: 시스템에 비정상적인 상황이 발생. 예측이 어렵고 기본적으로 복구가 불가능함
  - e.g: OutOfMemoryError, StackOverflowError, etc
- **Exception**: 시스템에서 포착 가능하여 (try-catch) 복구 가능. 예외 처리 강제
  - IOException, FileNotFoundException, etc
  - @Transactional 에서 해당 예외가 발생하면 기본적으로 롤백이 동작하지 않음
  - rollbackFor를 사용해야 함
- **RuntimeException**: 런타임시에 발생하는 예외. 예외 처리를 강제하지 않음
  - e.g: NullPointerException, ArrayIndexOUtOfBoundsException, etc


### 자바에서 Checked Exception은 컴파일 에러가 발생하기 때문에 무조건 try-catch로 감싸거나 throws로 예외를 전파해야 한다

```text
try {
    Thread.sleep(1)	
} catch (InterruptedException e) {
    // 예외 처리 
}
```


### 코틀린은 Checked Exception을 강제하지 않는다
- 아래의 코드는 코틀린에서 컴파일 오류가 발생하지 않는다

```text
Thread.sleep(1);
```