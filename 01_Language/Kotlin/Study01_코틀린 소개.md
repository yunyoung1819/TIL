# :pushpin: Chapter 01. 코틀린 소개


## 코틀린의 현재와 미래
### 코틀린을 배워야하는 이유
- 코틀린은 IntelliJ로 유명한 젯브레인사에서 만든 언어
- 자바에 비해 문법이 간결하기 때문에 가독성과 생산성이 높고 오류 가능성이 적어진다.


```kotlin
data class Person(
    val name: String,
    val age: Int,
    val email: String
)

object MyCompany {
    const val name: String = "MyCompany"
}

// 탑-레벨 함수로 클래스 외부에서 함수 작성 가능
fun main() {
    // 'new' 키워드 없이 객체 생성
    val person = Person("YUN YOUNG", 30, "test@co.kr")
    println(person)
}
```

### 유명 오픈 소스 프로젝트의 코틀린 프로젝트 지원 현황
- 스프링 프레임워크
- Gradle
- Ktor (젯브레인사에서 코틀린으로 만든 서버 프레임워크)
- Exposed