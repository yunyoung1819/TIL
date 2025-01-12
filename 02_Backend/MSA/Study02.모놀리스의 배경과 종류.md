# :book: 간편 결제 프로젝트로 한 번에 끝내는 실전 MSA

## :pushpin: Chapter 01. MSA가 왜 좋은거죠?

### 싱글 모듈 / 멀티모듈 아키텍처 
- 모놀리식 아키텍처에서 모듈을 구성하는 방식이 다름
- 대표적으로 싱글/멀티 모듈 아키텍처가 존재하고 특징이 조금 다름

### 싱글모듈
- 모든 소스가 단일 모듈 내에 존재
- 응집성과 결합도가 매우 높음
- 설계/구현이 간단하고 단순
- 최상위 싱글 패키지
- 유연성, 확장성이 제한적임

### 멀티모듈
- 역할, 서비스 별로 모듈화 되어 있음
- 응집성과 결합도가 낮은 편임
- 모듈 간 인터페이스 정의 필요 (아키텍처와도 밀접한 관련)
- 최상위 멀티 패키지
- 유연성, 확장성이 비교적 좋음 

### 싱글모듈 아키텍처
```
com.fastcampus.controller (Controller)
com.fastcampus.model (Model)
com.fastcampus.web (View)
...
```
- 1 Jar file

### 멀티모듈 아키텍처
```
com.fastcampus.user.controller (Controller)
com.fastcampus.user.model (Model)
com.fastcampus.user.web (Web)

com.fastcampus.lecture.controller (Controller)
com.fastcampus.lecture.model (Model)
com.fastcampus.lecture.web (Web)
```
- N jar files
- java -jar test1.jar test2.jar test3.jar -Xmx1024m -Xms1024m ...