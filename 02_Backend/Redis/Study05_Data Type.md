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


### Java 애플리케이션에서 Redis Client 사용하기

build.gradle
```text
dependencies {
    implementation 'redis.clients:jedis:4.3.1'
    testImplementation platform('org.junit:junit-bom:5.10.0')
    testImplementation 'org.junit.jupiter:junit-jupiter'
}
```

Main.java
```java
package org.example;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.Pipeline;

import java.util.List;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");

        try (var jedisPool = new JedisPool("127.0.0.1", 6379)) {
            try (Jedis jedis = jedisPool.getResource()) {
                jedis.set("users:300:email", "yujin@fastcompus.co.kr");
                jedis.set("users:300:name", "Cho Yu Jin");
                jedis.set("users:300:age", "20");

                var userEmail = jedis.get("users:300:email");
                System.out.println(userEmail);

                List<String> userInfo = jedis.mget("users:300:email", "users:300:name", "users:300:age");
                userInfo.forEach(System.out::println);

                long counter = jedis.incr("counter");
                System.out.println(counter);

                counter = jedis.incrBy("counter", 10L);
                System.out.println(counter);

                counter = jedis.decr("counter");
                System.out.println(counter);

                Pipeline pipelined = jedis.pipelined();
                pipelined.set("users:400:email", "zero@fastcomapus.co.kr");
                pipelined.set("users:400:name", "zero");
                pipelined.set("users:400:age", "37");
                List<Object> objects = pipelined.syncAndReturnAll();
                objects.forEach(i -> System.out.println(i.toString()));
            }
        }
    }
}
```