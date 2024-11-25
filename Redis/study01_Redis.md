## :pushpin: Redis


### :seedling: in-memory database
- in-memory: 컴퓨터의 메인 메모리
- 메모리에 데이터를 적재하여 활용하는 데이터베이스 시스템

#### 주요 특징
1. Millisecond response (1ms = 0.001s)
2. Volatility of RAM
3. Data types

#### Memory vs Disk
Memory read/writer 100만번 테스트
```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

class MemoryReadWriter {
    public static void main(String[] args) {
       String sample = "This is sample string";
        List arrayList = new ArrayList();

        long start = System.currentTimeMillis();
        for (int i = 0; i < 1_000_000; i++) {
            arrayList.add(sample);
        }

        arrayList.stream().collect(Collectors.toList());

        long end = System.currentTimeMillis();
        System.out.println("Execution time: " + (end - start) + " ms");
    }
}
```

Disk read/writer 100만번 테스트
```java
import java.io.*;

class FileReadWriter {
    public static void main(String[] args) {
        final var filename = "clip01.txt";
        final var sample = "this is sample";
        File file = new File(filename);

        long start = System.currentTimeMillis();

        try {
            OutputStream os = new FileOutputStream(file);
            PrintWriter writer = new PrintWriter(os);

            for (int i = 0; i < 1_000_000; i++) {
                writer.println(sample);
            }

            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
Memory, Disk read/write 100만번 테스트

| Memory | Disk |
| --- | --- |
| 1회차 17ms | 1회차 407ms |
| 2회차 17ms | 2회차 420ms |
| 3회차 29ms | 3회차 370ms |


#### In-memory Database 오픈소스
- Memcached (분산 저장소로 단일 데이터 타입만 제공)
  - Cache
- Redis (분산 저장소로 다양한 자료 구조 지원)
  - Cache
  - Session Store
  - Pub/Sub
  - Leader board
  - Geospatial


#### In-memory Database 마무리
1.. 메인 메모리
2. 빠른 응답속도, 높은 처리량
3. memcaced, redis