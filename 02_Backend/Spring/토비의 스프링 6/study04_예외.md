# pushpin: 토비의 스프링6
## :seedling: 예외

### 예외
- 예외는 정상적인 프로그램 흐름을 방해하는 사건
- 예외적인 상황에서만 사용
- 많은 경우 예외는 프로그램 오류, 버그 때문에 발생

#### 예외가 발생하면 
- 예외 상황을 복구해서 정상적인 흐름으로 전환할 수 있는가?
  - a. 재시도
  - b. 대안
- 버그인가?
  - a. 예외가 발생한 코드의 버그인가?
  - b. 클라이언트의 버그인가?
- 제어할 수 없는 예외 상황인가?


#### 예외를 잘못 다루는 코드
- 예외를 무시하는 코드

```text
try {

} catch(SQLException e) {
}

} catch (SQLException e) {
  e.printStackTrace();
}
```

- 무의미하고 무책임한 throws
```text
public void method1() throws Exception {
  method2();
}

public void method2() throws Exception {
  method3();
}

public void method3() throws Exception {

}

```

#### 예외의 종류
- Error
- Exception (checked)
- RuntimeException (unchecked)

#### Error
- 시스템에 비정상적인 상황이 발생
- `OutOfMemoryError`
- `ThreadDeath`

#### 체크 예외(Exception)
- `catch`나 `throws`를 강요
- 초기 라이브러리의 잘못된 예외 설계/사용
- 복구할 수 없다면 `RuntimeException`이나 적절한 추상화 레벨의 예외로 전환해서 던질 것

#### 예외의 추상화와 전환
- 사용 기술에 따라 같은 문제에 대해 다른 종류의 예외 발생
- 적절한 예외 추상화와 예외 번역이 필요
