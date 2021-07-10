# :book: 엘라스틱서치 쿡북

###### 엘라스틱서치 쿡북을 읽고 그 내용을 요약한 글 입니다. 상세 내용은 책을 참조해주세요.

---------------------------------------------------------------------------

## :pushpin: 2장. 다운로드와 설정

### 일래스틱서치 패키지

- bin: 일래스틱서치를 시작하고 관리하는 스크립트가 있다.
- config: 일래스틱 서치 설정을 포함
    - elasticsearch.yml: 일래스틱서치의 주요 설정 파일
    - log4j2.properties: 로깅 설정 파일
- lib: 일래스틱서치를 실행하는데 필수적인 라이브러리
- modules: 일래스틱서치 기본 확장 모듈
- plugins: 설치한 플러그인 


### 네트워킹 관리 
- cluster.name은 클러스터 이름을 설정한다. 같은 클러스터 이름을 가진 노드만 서로 결합할 수 있다.

### 다양한 노드 타입 설정
- 마스터 노드 여부를 설정한다.

```
node.master: true
```

- 데이터를 갖는 노드인지 설정한다.
```
node.data: true
```

- 수집 노드 설정 
```
node.injest: true
```

- 로깅 설정 변경 (log4j2.properties 파라미터를 변경)
````
rootLoger.level = info
````