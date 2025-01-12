# :book: selab-study
## :pushpin: Topic. AOP 


### AOP (Aspect Oriented Programming)

- 관점 지향 프로그래밍
- 비즈니스 로직의 기준을 정하고 그 기준에 따라 나눈 부분을 관점이라고 한다면 이 관점을 모듈화하는 것

### AOP 용어
- Aspect: 여러 클래스에서 중복적으로 사용되는 공통된 관점을 모듈화한 것
- JoinPoint: method 또는 exception와 같은 끼어들 수 있는 지점
- Pointcut: 특정 JoinPoint에서 Aspect가 적용할 Advice를 일치시키기 위한 것
- Advice: 특정 JoinPoint에서 Aspect가 한 액션
- Target: Aspect를 적용하는 지점