## 프론트엔드 개발환경의 이해 NPM


### 프론트엔드 개발에 Node.js가 필요한 이유
- 최신 스펙으로 개발할 수 있다
- 빌드 자동화
- 개발 환경 커스터마이징


### Node.js 설치

- Nodejs.org 사이트에서 운영체제 별로 설치파일을 다운로드받는다.
- 버튼을 몇 번 클릭하면 아래 경로에 Node.js 와 NPM이 설치된다.

- Node.js: /usr/local/bin/node
- NPM: /usr/local/bin/npm

```
$node
> 1 + 2
3
```

```
$node --version
v13.1.0
```

```
$npm --version
6.12.1
```

### 프로젝트 초기화

- 개발 프로젝트는 외부 라이브러리를 다운로드 받고 빌드하는 등 일련의 명령어를 자동화하여 프로젝트를 관리하는 도구가 존재
- PHP의 컴포져(Composer)나 자바의 그래들(Gradle) 같은 툴이 그러한 프로그램이다.
- NPM은 자바스크립트 기반 프로젝트의 빌드 도구이다.


#### INIT

- NPM은 다양한 하위 명령어를 제공하는데 그중 init 명령을 사용하면 프로젝트를 생성할 수 있다.

```
$npm init
```

#### Package.json

- Node.js는 package.json 파일에 프로젝트의 모든 정보를 기록한다.

```
name: 프로젝트 이름
version: 프로젝트 버전 정보
description: 프로젝트 설명
main: 노드 어플리케이션일 경우 진입점 경로, 프론트엔드 프로젝트일 경우 사용하지 않는다.
script: 프로젝트 명령어를 등록할 수 있다.
author: 프로그램 작성자
license: 라이센스
```

#### 프로젝트 명령어
- 생성한 프로젝트는 package.json에 등록한 스크립트를 이용해 실행한다.


