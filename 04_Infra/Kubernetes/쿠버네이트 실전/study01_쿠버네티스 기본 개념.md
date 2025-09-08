# :book: 인프런 - 쿠버네티스 강의
## :pushpin: 쿠버네티스 입문/실전편


### 쿠버네티스란?
쿠버네티스(Kubernetes)란?
- 쿠버네티스는 *다수의 컨테이너를 효율적으로 배포, 확장 및 관리*하기 위한 오픈 소스 시스템이다.
- 쿠버네티스는 Docker Compose와 비슷한 느낌을 가지고 있다. Docker Compose도 다수의 컨테이너를 쉽게 관리하기 위해 활용하기 때문

쿠버네티스의 장점 
- 컨테이너 관리 자동화 (배포, 확장, 업데이트)
- 부하 분산 (로드밸런싱)
- 쉬운 스케일링
- 셀프 힐링


### 로컬에서의 쿠버네티스 설치 (Docker Desktop)
- 1. Docket Desktop을 활용해서 쿠버네티스를 설치해서 사용
- 2. kubectl 설치
  - kubectl (Kubernetes Control)의 줄임말: 쿠버네티스에 명령어를 입력할 수 있게 해주는 CLI 툴
- 3. 잘 작동하는지 확인
  - kubectl version

kubenetes 설치 link: https://soojae.tistory.com/87
kubectl 설치 link: https://kubernetes.io/ko/docs/tasks/tools/install-kubectl-macos/
  

### 파드(Pod)란?
- 도커에서는 하나의 프로그램을 실행시키는 단위를 `컨테이너`라고 불렀음
- 쿠버네티스에서는 하나의 프로그램을 실행시키는 단위를 `파드(Pod)`라고 한다.
- 파드(Pod): **쿠버네티스에서 하나의 프로그램을 실행시키는 단위**
  - 쿠버네티스에서 가장 작은 단위
  - 일반적으로 하나의 파드가 하나의 컨테이너를 가진다.
  - 예외적으로 하나의 파드가 여러 개의 컨테이너를 가지는 경우도 있다.
  
![](../images/kube01.png)
- 2개의 결제 서버가 띄워져 있다 = 2개의 결제 서버 파드(Pod)가 띄워져있다.
- 1개의 결제 서버가 죽었다 = 1개의 결제 서버 파드(Pod)가 죽었다
- 업로드 서버를 하나 띄우자 = 업로드 서버 하나를 파드(Pod)로 띄우자


### 웹 서버(Nginx)를 파드(Pod)로 띄워보기
- 파드(Pod)를 생성할 때 CLI를 활용하는 방법이 있고 yaml 파일을 활용하는 방법이 있다.
- 실제 현업에서는 yaml 파일을 활용하는 경우가 많다. 따라서 yaml 파일을 활용해서 파드(Pod)를 생성해볼 것이다.

nginx-pod.yaml
````
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx-container
      image: nginx
      ports:
        - containerPort: 80
````

```
kubectl apply -f nginx-pod.yaml

kubectl get pods
```

- yaml 파일: 매니페스트 파일(Manifest File)