# :book: 백엔드 개발자를 위한 대용량 데이터 & 트래픽 처리
## :pushpin: Chapter 08. 커버링 인덱스

### 인덱스
![](./images/인덱스1.png)
![](./images/인덱스2.png)

### 커버링 인덱스
- 검색조건이 인덱스에 부합한다면, 테이블에 바로 접근하는 것보다 인덱스를 통해 접근하는 것이 매우 빠르다.
- 그렇다면 테이블에 접근하지 않고 인덱스로만 데이터 응답을 내려줄 순 없을까?

````text
SELECT 나이
FROM 회원
WHERE 나이 < 30
````

![](./images/커버링인덱스.png)

````text
SELECT 나이, id
FROM 회원
WHERE 나이 < 30
````

- MySQL에서는 PK가 클러스터 인덱스이기 때문에 커버링 인덱스에 유리 

#### 커버링 인덱스로 페이지네이션 최적화를 어떻게 할 수 있을까?
- 나이가 30 이하인 회원의 이름을 2개만 조회

```text
with 커버링 as (
SELECT id
FROM 회원
WHERE 나이 < 30
LIMIT 2
)
```

```text
SELECT 이름
FROM 회원 INNER JOIN 커버링 on 회원.id = 커버링.id
```
- 데이터베이스의 랜덤 액세스를 줄임
- `order by`, `offset`, `limit` 절로 인한 불필요한 데이터블록 접근을 커버링 인덱스를 통해 최소화