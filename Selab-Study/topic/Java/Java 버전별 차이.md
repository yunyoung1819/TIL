# :book: selab-study 
## :pushpin: Topic. Java 버전 별 차이

### Java 버전 별 차이 및 특징

이번 포스팅에서는 자바 버전 별 차이 및 특징에 대해 포스팅하겠습니다.


#### Java 8

- Lambda
- Stream
- interface default method
- Optional 
- new Date and Time API (LocalDateTime)


#### Java 9

- 모듈 시스템 등장
- 컬렉션에 list, set, map을 쉽게 구성할 수 있는 몇 가지 추가 기능
- 스트림 takeWhile, dropWhile, iterate 메서드 형태로 몇 가지 추가 기능
- optional: ifPresentOrElse 추가 기능
- 인터페이스에 private method 사용 가능
- try-with-resources 문 


#### Java 10

- `var` 키워드 도입 
- `병렬 처리 가비지 컬렉션` 도입으로 인한 성능 향상
- JVM 힙 영역을 시스템 메모리가 아닌 다른 종류의 메모리에도 할당 가능


#### Java 11

- Oracle JDK와 Open JDK 통합
- Oracle JDK가 구독형 유료 모델로 전환
- 서드파티 JDK로의 이전 필요
- lambda 지역변수 사용법 변경
- Strings and Files에는 몇 가지 새로운 메서드 추가
- Run Source Files
    - Java 10부터 Java 소스 파일을 먼저 컴파일 하지 않고도 실행할 수 있음
    - 스크립팅을 향한 한걸음
- 람다 매개변수에 대한 지역 변수 유형 추론 (var)


#### Java 13

- `스위치 표현식` (Preview)
- `Multiline Strings` (Preview)


#### Java 14

- 스위치 표현식 표준화
- instanceof 패턴 매칭
- `record` 선언 기능 추가 


#### Java 15

- `Text-Blocks` / `Multiline Strings`
- `Records` & `Pattern Matching`


#### Java 16

- Pattern Matching for instanceof
- Unix-Domain Socket Channels
- Foreign Linker API


#### Java 17

- Pattern Matching for switch
- Sealed Classes
- Foreign Function & Memory API
- Deprecating the Security Manager