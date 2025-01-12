# :book: 스프링 부트 개념과 활용 (백기선)

## :pushpin: 내장 웹 서버 이해

### 내장 서블릿 컨테이너
- 스프링 부트는 서버가 아니다.
    - 톰캣 객체 생성
    - 포트 설정
    - 톰캣에 컨텍스트 추가
    - 서블릿 만들기
    - 톰캣에 서블릿 추가
    - 컨텍스트에 서블릿 맵핑
    - 톰캣 실행 및 대기

- 이 모든 과정을 보다 상세히 또 유연하고 설정하고 실행해주는게 바로 스프링 부트의 자동 설정.
    - ServletWebServerFactoryAutoConfiguration (서블릿 웹 서버 생성)
        - TomcatServletWebServerFactoryCustomizer (서버 커스터마이징)
    - DispatcherServletAutoConfiguration
        - 서블릿 만들고 등록
