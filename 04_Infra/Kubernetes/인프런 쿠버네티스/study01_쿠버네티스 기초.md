# :book: 인프런 - 쿠버네티스 강의
## :pushpin: 기초편

### Introduction

```text
Linux (자원 격리 기술) -> VM (가상화 기술) -> Container (가상화 기술) -> Container (오케스트레이터) -> Kubernetes (클라우드 서비스)
```

- 서버 자원을 효율적으로 쓰기 위해서는 가상화 기술에 대한 관심을 가질 수 밖에 없음
- 컨테이너 가상화 기술은 서비스 간에 자원 격리를 하는데 OS를 별도로 안 띄워도 됨
- OS 기동 시간이 없기 때문에 자동화 시 엄청 빠르고 자원 효율도 매우 높음 
- 도커 자체는 하나의 서비스를 컨테이너로 가상화시켜서 배포를 하는 것이고, 엄청 많은 서비스들을 운영할 때 일일이 배포하고 운영하는 역할을 해주지 않음.
- 이런 것을 해주는 것이 `컨테이너 오케스트레이터`라는 개념으로 *여러 컨테니어들을 관리해주는 솔루션*

![](images/1.png)

### Why Kubernetes?

![](images/2.png)

### VM vs Container

![](images/01.png)

VM
- Host Server
- Host OS
- Hypervisor
- Guest OS
- A Service

Container
- Host Server
- Host OS
- docker / rkt / LXC

