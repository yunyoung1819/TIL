# :pushpin: 코틀린 코루틴 완전 정복

## :seedling: 스레드 기반 작업의 한계와 코루틴의 등장

### 1. JVM의 프로세스와 스레드
- Kotlin 애플리케이션의 실행 진입점은 main 함수를 통해 만들어진다.
- main 함수를 실행 요청하면, JVM은 프로세스를 시작하고 메인(main) 스레드를 생성해 코드를 실행한 후 종료한다.

```kotlin
fun main() {
    println("[${Thread.currentThread().name}] 시작")
    Thread.sleep(1000L)
    println("[${Thread.currentThread().name}] 종료")
}
```

![img.png](./img/img.png)