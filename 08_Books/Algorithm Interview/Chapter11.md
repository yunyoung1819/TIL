## :pushpin: 프로그래머스 코딩테스트 문제 풀이 전략:자바편

### 11장.자주 등장하는 자료 구조
#### 스택과 큐

스택과 큐 두 가지는 원소를 특정한 순서대로 삽입하고 제거할 수 있는 자료구조로 다음 연산을 제공합니다.
1. 원소 삽입
2. 원소 제거
3. 자료 구조가 비어 있는지 검사

#### 스택
- 스택은 LIFO(Last In First Out: 후입선출) 특징이 있는 자료 구조
- 자바에서는 스택을 내장 제네릭 클래스로 지원한다.
- 정수를 담을 수 있는 스택은 다음과 같이 선언할 수 있다.

```java
Stack<Integer> stack = new Stack<>();
```

- 원소 추가는 add() 메서드, 삭제는 pop() 메서드로 할 수 있다.
- pop() 메서드를 호출하면 제거된 원소가 반환된다.
- 주의해야할 점은 스택이 비어 있는 상태에서 원소를 제거하는 pop() 메서드를 호출하면 `EmptyStackException`이 발생한다.
- 스택이 비어있는지 여부는 isEmpty() 메서드로 확인할 수 있다.
- peek() 메서드로 스택에서 값을 제거하지 않고도 스택의 가장 위에 있는 값을 얻을 수 있다.
- 스택을 활용하는 문제에서는 주로 짝을 찾는 용도로 스택을 활용한다.


#### 큐
- 큐(queue)는 스택과 비슷하게 생긴 자료 구조
- 스택이 긴 바구니였다면 큐는 긴 빨대이다. 빨대는 양쪽이 뚫려 있기 때문에 한쪽으로는 원소가 삽입되고 다른 쪽으로는 빠져나가게 된다.
- 먼저 삽입한 원소가 먼저 나오는 구조를 `FIFO(First In First Out: 선입선출)`라고 한다.
- 자바에서 큐는 스택과는 다르게 인터페이스로 작성되어 있다. 따라서 자바에서 큐를 이용하려면 인터페이스 Queue를 구현하는 클래스를 사용한다.
  - 이를 위해 가장 많이 활용되는 클래스는 LinkedList 이다.
  - 다음과 같이 LinkedList 클래스를 사용하여 Queue를 선언할 수 있다.

```text
Queue<Integer> queue = new LinkedList<>();
```

- Queue 인터페이ㅡ가 제공하는 add()와 poll() 메서드를 사용하면 다음과 같이 원소를 삽입하고 제거할 수 있다.

```text
Queue<Integer> queue = new LinkedList<>();

queue.add(1);
queue.add(2);
queue.add(3);

System.out.println(queue.poll()); // 1
System.out.println(queue.poll()); // 2

queue.add(4);
System.out.println(queue.poll()); // 3
System.out.println(queue.isEmpty()); // false

System.out.println(queue.poll()); // 4
System.out.println(queue.isEmpty()); // true
```

- 또 Stack과 마찬가지로 isEmpty() 메서드를 사용하여 자료구조가 비어 있는지 확인할 수 있다.
