## :pushpin: Redis

### :seedling: Redis 설치

#### Docker Container 기반으로 redis 설치하기 (Docker hub)

터미널을 열고 아래와 같이 Command 명령어를 입력한다.

```shell
1. docker pull redis:6.2
2. docker images 
3. docker run --rm [IMAGE:VERSION] (컨테이너 실행)
   - ex) docker run --rm -it redis:6.2
4. docker run --rm -it -d [IMAGE:VERSION] (백그라운드 실행)
   - ex) docker run --rm -it -d redis:6.2
5. docker ps
6. docker run --rm -it -d -p [PORT:PORT][IMAGE:VERSION] (포트 설정)
   - ex) docker run --rm -it -d -p 6379:6379 redis:6.2
7. docker kill [Container ID] (컨테이너 종료)

```

