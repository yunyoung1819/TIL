## Virtual Thread 란?

- Virtual Thread == 자바 진영의 경량 스레드 모델

- Virtual Thread의 특징
  - 메모리 사용량이 적다
  - 최대 개수가 아주 ~~ 많다
  - 스레드 생성 비용이 싸다
  - 컨텍스트 스위칭 및 스케줄링 비용이 싸다
  - Nonblocking I/O를 지원
  - OS 스레드와 N:M 관계
  - 시스템 콜 안함

- Nonblocking I/O
    - I/O 작업으로 인한 Blocking 시간 동안 대기하지 않고 다른 작업을 처리하는 것 

- 결론
  - Virtual Thread를 사용하면 기존 구조를 유지하면서 처리량을 높일 수 있다.

- 사용 시 유의사항
  - pinning: 캐리어 스레드가 block 당하는 것 
  - CPU bound 작업: 오히려 방해
  - 과도한 트래픽 전파: timeout