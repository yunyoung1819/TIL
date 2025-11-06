## :pushpin: 프로그래머스 코딩테스트 문제 풀이 전략: 자바편

### 7장. :seedling: 정렬
- 데이터가 들어있는 리스트를 정렬하는 것은 단순히 리스트를 전부 순회하는 것 이상의 시간이 필요
- 리스크 길이를 `N`이라고 할 때, 리스트를 순회하는 것은 선형 시간 복잡도인 `O(N)`이 소요되는 반면 정렬은 `O(N logN)`이 소요
- 정렬에는 `선택 정렬`, `삽입 정렬`, `퀵 정렬`, `힙 정렬` 등 아주 많은 종류의 알고리즘이 있음

#### 여러 정렬 알고리즘의 시간 복잡도

| 종류    | 최악의 경우 시간 복잡도 |
|-------|---------------|
| 버블 정렬 | O(N^2)        |
| 선택 정렬 | O(N^2)        |
| 삽입 정렬 | O(N^2)        |
| 퀵 정렬  | O(N^2)        |
| 힙 정렬  | O(N logN)     |
| 병합 정렬 | O(N logN)     |


#### 정렬하기
- 정렬에는 여러 방법이 있음
- 코딩 테스트에서는 최악의 경우를 상정하고 문제를 해결해야 하기 때문에 최악의 경우 시간 복잡도만 빠면 된다.
- 자바는 내장 정렬 메서드를 제공하므로 이런 정렬 방법들을 기본적으로 구현할 필요가 없음
- 자바의 내장 정렬 메서드는 위에서 언급한 기본 정렬 방법들을 개량한 정렬 알고리즘을 사용하기 때문에 O(N logN)의 시간 복잡도를 기대할 수 있다.
  - 배열: `Arrays.sort()` 전달받은 배열 자체를 정렬
  - List, Vector: `Collection.sort()` 전달받은 Collection 자체를 정렬
  - Stream: `stream.sorted()` 정렬된 Stream을 반환

```text
int[] array = {5, 10, 7, 9, 3, 2};
Arrays,sort(array);  // [2, 3, 5, 7, 9, 10]
System.out.println(Arrays.toString(array));

List<Integer> collection = new ArrayList<>(List.of(5,10,7,9,3,2));
Collections.sort(collection);
System.out.println(collection);

Stream<Integer> stream = Stream.of(5, 10, 7, 9, 3, 2).sorted();
System.out.println(stream.collect(Collectors.toList()));
```

- Arrays.sort()와 Collections.sort()는 전달받은 객체 자체를 정렬한다.
- stream.sorted() 메서드는 정렬된 Stream을 반환 
- 내장 메서드들은 기본 정렬 기준에 따라 정렬을 수행한다.
  - 숫자형: 오름차순 (`int`, `long`, `char`, `double`, `float`, ...)
  - 문자열: 사전순 (`String`)