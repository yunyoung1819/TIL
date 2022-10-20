# :book: selab-study
## :pushpin: Topic. Java 컬렉션 (Collection)

### Collection이란?

- 자바에서 컬렉션(collection)이란 다수의 데이터를 쉽고 효율적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합을 의미
- 즉 데이터를 저장하는 자료 구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은 것
- 컬렉션 프레임워크는 자바의 인터페이스(interface)를 사용하여 구현함

### Java 컬렉션 프레임워크 상속 구조

![](../images/컬렉션.PNG)

- Collection  인터페이스는 List, Set, Queue로 크게 3가지 상위 인터페이스로 분류할 수 있음
- Map의 경우 Collection 인터페이스를 상속받고 있지는 않지만 Collection으로 분류됨


### Collection 인터페이스의 특징

|인터페이스|구현 클래스|특징|
|----------|----------|----------|
|Set|HashSet, TreeSet|순서를 유지하지 않는 데이터의 집합으로 데이터의 중복을 허용하지 않음|
|List|LinkedList, Vector, ArrayList|순서가 있는 데이터의 집합으로 데이터의 중복을 허용함|
|Map|HashTable,HashMap,TreeMap|키(Key),값(Value)의 쌍으로 이루어진 데이터의 집합으로 순서는 유지되지 않으며 키의 중복을 허용하지 않으나 값의 중복은 허용함|


### List
- ArrayList
    - 동적 배열을 제공
    - 컬렉션에서 개체를 추가, 삭제하면 ArrayList의 크기가 자동으로 조정됨

```java
import java.io.*;
import java.util.*;
  
class ArrayListTest {
    public static void main(String[] args)
    {
  
        // ArrayList 선언
        ArrayList<Integer> al
            = new ArrayList<Integer>();
  
        // ArrayList에 데이터 입력
        for (int i = 1; i <= 5; i++)
            al.add(i);
  
        // 결과 출력
        System.out.println(al);
  
        // 3번 데이터 제거
        al.remove(3);
  
        // 결과 출력
        System.out.println(al);
  
        // 하나씩 가져와서 결과 출력
        for (int i = 0; i < al.size(); i++)
            System.out.print(al.get(i) + " ");
    }
}
```
    
- LinkedList
  - 요소가 연속된 위치에 저장되지 않고 모든 요소가 데이터 부분과 주소 부분이 있는 별도의 객체에 저장됨
  - 포인터와 주소를 사용해서 데이터를 가져옴
  - 각 요소를 노드라고 부름

```java
import java.io.*;
import java.util.*;
  
class LinkedListTest {
    public static void main(String[] args)
    {
  
        // LinkedList 선언
        LinkedList<Integer> ll
            = new LinkedList<Integer>();
  
        // 값 입력
        for (int i = 1; i <= 5; i++)
            ll.add(i);
  
        // 결과 출력
        System.out.println(ll);
  
        // 3번 데이터 삭제
        ll.remove(3);
  
        // 결과 출력
        System.out.println(ll);
  
        // 결과를 하나씩 출력
        for (int i = 0; i < ll.size(); i++)
            System.out.print(ll.get(i) + " ");
    }
}
```
  
- Vector
    - 동적 배열을 제공하고 표준 배열보다 느리지만 많은 움직임이 필요한 프로그램에서 유용
    - ArrayList와 유사함

````java
import java.io.*;
import java.util.*;
  
class VectorTest {
    public static void main(String[] args)
    {
  
        // Vector 선언
        Vector<Integer> v
            = new Vector<Integer>();
  
        // 데이터 입력
        for (int i = 1; i <= 5; i++)
            v.add(i);
  
        // 결과 출력
        System.out.println(v);
  
        // 3번 데이터 삭제
        v.remove(3);
  
        // 결과 출력
        System.out.println(v);
  
        // 하나씩 결과 출력
        for (int i = 0; i < v.size(); i++)
            System.out.print(v.get(i) + " ");
    }
}
````

### Set
- HashSet
  - HashSet에 입력되는 데이터는 동일한 순서로 삽입되는 것을 보장하지 않음
  - NULL 요소 삽입을 허용함

````java
import java.util.*;
public class HashSetDemo {
    public static void main(String args[])
    {
        // HashSet 선언 및 데이터 입력
        HashSet<String> hs = new HashSet<String>();
  
        hs.add("Hello");
        hs.add("World");
        hs.add("Hello");
        hs.add("Blog");
        hs.add("CrazyKim");
  
        // Traversing elements
        Iterator<String> itr = hs.iterator();
        while (itr.hasNext()) {
            System.out.println(itr.next());
        }
    }
}
````

- LinkedHashSet
  - HashSet과 유사하지만 차이점은 데이터를 저장하는 순서를 유지함

````java
import java.util.*;
public class LinkedHashSetDemo {
    public static void main(String args[])
    {
        // LinkedHashSet 선언 및 데이터 입력
        LinkedHashSet<String> lhs
            = new LinkedHashSet<String>();
  
        lhs.add("Hello");
        lhs.add("World");
        lhs.add("Hello");
        lhs.add("blog");
        lhs.add("CrazyKim");
  
        // 결과 출력
        Iterator<String> itr = lhs.iterator();
        while (itr.hasNext()) {
            System.out.println(itr.next());
        }
    }
}
````

- TreeSet
  - Tree를 사용하여 저장함
  - 데이터의 순서는 자연적인 순서(오름차순)대로 유지가 됨

````java
import java.util.*;
public class TreeSetDemo {
    public static void main(String args[])
    {
        // TreeSet 변수 선언 및 데이터 입력
        TreeSet<String> ts
            = new TreeSet<String>();
  
        ts.add("Hello");
        ts.add("World");
        ts.add("Hello");
        ts.add("Blog");
        ts.add("CrazyKim");
  
        // Traversing elements
        Iterator<String> itr = ts.iterator();
        while (itr.hasNext()) {
            System.out.println(itr.next());
        }
    }
}
````

### Map
- HashMap
  - 데이터를 키 - 값 형태로 저장함
  - HashMap은 Hashing이라는 기술을 사용하는데 해싱은 인덱싱 및 검색 작업이 더 빨라지도록 키에 산술적인 연산을 적용하여
  항목이 저장되어 있는 테이블의 주소를 계산하여 항목에 접근하는 방식

````java
import java.util.*;
public class HashMapDemo {
    public static void main(String args[])
    {
        // HashMap 선언 및 데이터 입력
        HashMap<Integer, String> hm
            = new HashMap<Integer, String>();
  
        hm.put(1, "Hello");
        hm.put(2, "World");
        hm.put(3, "CrazyKim");
  
        // 첫 번째 결과 출력
        System.out.println("Value for 1 is " + hm.get(1));
  
        // 전체 결과 출력
        for (Map.Entry<Integer, String> e : hm.entrySet())
            System.out.println(e.getKey() + " " + e.getValue());
    }
}
````
