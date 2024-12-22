## :pushpin: Redis
### :seedling: Data Type
Key / Value
- Key
  - binary and text 
  - ex) "name", "123", "#!:()"
- Value
  - Strings
  - Lists
  - Sets
  - Sorted sets
  - Hashes
  - Geospatial
  - Bitmap

#### Strings
대표 기본 타입으로 바이너리, 문자 데이터를 저장
- maximum 512MB

증가 감소에 대한 원자적 연산
- increment / decrement

command
  - SET
  - SETNX
  - GET
  - MGET
  - INC
  - DEC

```shell
SET users:1:email zero@fastcampus.co.kr
OK
GET users:1:email
"zero@fastcampus.co.kr"
```
```
INCR counter
(integer) 1
INCR counter
(integer) 2
```

잠깐 Key 명령어를 알아 봅시다
- TTL (Time To Live)
  - EXPIRE [KEY] [SECOND]
  - TTL [KEY]

- DEL (sync)
- **UNLINK** (async적으로 삭제)
- MEMORY USAGE 


#### Lists
- Linked List (strings)
  - 예) Java ArrayList
- Queue, Stack
- command
  - LPUSH
  - RPUSH
  - LPOP
  - RPOP
  - LLEN
  - LRANGE


#### Sets
- Unordered collection (unique strings)
  - 예) Java Set
- Unique item
  - SNS follow
  - Blacklist
  - Tags
- command
  - SADD
  - SREM
  - SISMEMBER
  - SMEMBERS
  - SINTER
  - SCARD

> sadd users:1:posts:100:tags java

#### Sorted Set
- ordered collection (unique strings)
  - 예) java Sorted Set
- Leader board
- Rate limit

- command
  - ZADD
  - ZREM
  - ZRANGE
  - ZCARD
  - ZRANK / ZREVRANK
  - ZINCRBY

#### Hashes
- field-value pair collections 
- 예) Java HashMap
- command
  - HSET
  - HGET, HMGET
  - HGETALL
  - HDEL
  - HINCRBY

### Geospatial
- Coordinate (Latitude and Longitude)
- command
- GEOADD
- GEOSEARCH
- GEODIST
- GEOPOS

### Bitmap
- 0 또는 1의 값으로 이루어진 비트열
- 메모리를 적게 사용하여 대량의 데이터 저장에 유용
- command
- SETBIT
- GETBIT
- BITCOUNT

### 마무리
Key / Value (Data type)
- Strings
- Lists
- Sets
- Sorted sets
- Hashes
- Geospatial
- Bitmap

