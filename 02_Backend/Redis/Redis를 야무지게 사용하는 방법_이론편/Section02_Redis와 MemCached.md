# :pushpin: Redis

## :seedling: Section 4. Redis와 MemCached
### MemCached
- Redis보다 더 빠르고 분산 데이터 처리가 가능하다.
- 더 적은 메타데이터를 사용하기 때문에 메모리 소비가 적다. (조금 더 빠르다)
- 다양한 타입을 지원하지 않고 데이터 영속성이 보장이 안된다. (문자열만 지원)
- 또한 시장의 파이가 Redis에 비해 작고 이로 인해서 업데이트 및 버그 수정이 느리다.

-> 그러니 맘 편하게 Redis를 사용하자

## :seedling: Section 5. 반드시 알아야하는 캐싱 전략

### 캐싱 전략 Look_Aside
![image](../images/look_aside.png)

- 읽기 작업에 최적화되어 있다.
- 캐시가 있다면 캐시를 내려주고, 없다면 DB를 조회 후 캐시를 재설정 및 결과로 사용한다.
- 과도한 트래픽 상황 즉 Thundering Herd 상황에 대해서 갑작스런 DB 부하가 몰릴 수 있으니 캐시 조회 시에 TTL을 확인하여 재할당하거나 다른 방어 로직을 추가해두자.