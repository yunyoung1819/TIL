## chapter 2. 의미 있는 이름


### 들어가면서

- 소프트웨어에서 이름은 어디나 쓰인다.
- 많이 사용하므로 이름을 잘 지으면 여러모로 편하다.
- 이 장에서는 이름을 잘 짓는 간단한 규칙을 몇 가지 소개한다.


### 의도를 분명하게 밝혀라

- 좋은 이름을 지으려면 시간이 걸리지만 좋은 이름으로 절약하는 시간이 훨씬 더 많다.
- 변수나 함수 그리고 클래스 이름은 다음과 같은 굵직한 질문에 모두 답해야 한다.
- 변수 (혹은 함수나 클래스)의 존재 이유는? 수행 기능은? 사용 방법은? 
- 따로 주석이 필요하다면 의도를 분명히 드러내지 못했다는 말이다. 


```
int d;  // 경과 시간 (단위: 날짜)
```

- 이름 d는 아무 의미도 드러나지 않는다.
- 측정하려는 값과 단위를 표현하는 이름이 필요하다.

```
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```


- 의도가 드러나는 이름을 사용하면 코드 이해와 변경이 쉬어진다.

- 나쁜 코드
```
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList) 
        if (x[0] == 4)
            list1.add(x);
    return list1;
}
```

- 코드가 하는 일을 짐작하기 어렵다. 코드 맥락이 코드 자체에 명시적으로 드러나지 않는다.
- 각 개념에 이름만 붙여도 코드가 상당히 나아진다.

- 좋은 코드

```
public List<int[]> getFlaggedCells() {
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard)
        if (cell[STATUS_VALUE] == FLAGGED)
            flaggedCells.add(cell);
    return flaggedCells;
}
```

- 단순히 이름만 고쳤는데도 함수가 하는 일을 이해하기 쉬어졌다. 바로 이것이 좋은 이름이 주는 위력이다.


### 그릇된 정보를 피하라

- 프로그래머는 코드에 그릇돤 단서를 남겨서는 안된다.
- 나름대로 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용해도 안된다.
- 여러 계정을 그룹으로 묶을 때, 실제 List가 아니라면 accoutList라 명명하지 않는다.
- 계정을 담는 컨테이너가 실제 List가 아니라면 프로그래머에게 그릇된 정보를 제공하는 셈이다.
- 서로 흡사한 이름을 사용하지 않도록 주의한다.
- 유사한 개념은 유사한 표기법을 사용한다.
- 이름으로 그릇된 정보를 제공하는 진짜 끔찍한 예가 소문자 l이나 대문자 O 변수다.
- 소문자 l은 숫자 1처럼 보이고 대문자 O는 숫자 0처럼 보인다.


### 의미 있게 구분하라

- 컴파일러는 통과할지라도 연속된 숫자를 덧붙이거나 불용어(noise word)를 추가하는 방식은 적절하지 못하다.
- 연속적인 숫자를 덧붙인 이름(a1, a2, ..., aN)은 의도적인 이름과 정반대다. 이런 이름은 그릇된 정보를 제공하는 이름도 아니며, 아무런 정보를 제공하지 못하는 이름일 뿐이다. 저자 의도가 전혀 드러나지 않는다.

```
public static void copyChars(char a1[], char a2[]) {
    for (int i = 0; i < a1.length; i++) {
        a2[i] = a1[i];
    }
}
```

- 함수 인수 이름으로 source와 definition을 사용한다면 코드 읽기가 훨씬 더 쉬워진다.
- 불용어를 추가한 이름 역시 아무런 정보도 제공하지 못한다.

```
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo():
```

- 이 프로젝트에 참여한 프로그래머는 어느 함수를 호출할지 어떻게 알까?
- 읽는 사람이 차이를 알도록 이름을 지어라


### 발음하기 쉬운 이름을 사용하라

- 발음하기 어려운 이름은 토론하기도 어렵다.
- 발음하기 쉬운 이름은 중요하다. 
- 프로그래밍은 사회 활동이기 때문이다. 


### 검색하기 쉬운 이름을 사용하라

- 변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 바람직하다.
- 이런 관점에서 긴 이름이 짧은 이름보다 좋다. 검색하기 쉬운 이름이 상수보다 좋다.
- WORK_DAYS_PER_WEEK를 찾기가 얼마나 쉬운지 생각해보라.
- 그냥 5를 사용한다면 5가 들어가는 이름을 모두 찾은 후 의미를 분석해 원하는 상수를 가려내야 한다.


### 인코딩을 피하라

- 유형이나 범위 정보까지 인코딩에 넣으면 그만큼 이름을 해독하기 어려워진다. 


### 자신의 기억력을 자랑하지마라

- 독자가 코드를 읽으면서 변수 이름을 자신이 아는 이름으로 변환해야 한다면 그 변수 이름은 바람직하지 못하다.
- 문자 하나만 사용하는 변수 이름은 문제가 있다. 
- 루프에서 반복 횟수를 세는 변수 i, j, k 는 괜찮다. (l은 절대 안된다)
- 단, 루프 범위가 아주 작고 다른 이름과 충돌하지 않을 때만 괜찮다.
- 루프에서 반복 횟수 변수는 전통적으로 한 글자를 사용하기 때문이다.
- 그 외에는 대부분 적절하지 못하다. 독자가 실제 개념으로 변환해야 하니까. 


### 클래스 이름

- 클래스 이름과 객체 이름은 명사나 명사구가 적합낟. 
- Customer, WikiPage, Account, AddressParser 등이 좋은 예다.


### 메서드 이름

- 메서드 이름은 동사나 동사구가 적합하다.
- 접근자, 변경자, 조건자는 javabean 표준에 따라 값 앞에 get, set, is를 붙인다.


### 기발한 이름은 피하라

- 재미난 이름보다 명료한 이름을 선택하라.


### 한 개념에 한 단어를 사용하라

- 추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.
- 똑같은 메서드를 클래스마다 fetch, retrieve, get으로 제각각 부르면 혼란스럽다.


### 말장난을 하지 마라

- 한 단어를 두 가지 목적으로 사용하지 마라.


### 해법 영역에서 가져온 이름을 사용하라.

- 기술 개념에는 기술 이름이 가장 적합한 선택이다.


### 문제 영역에서 가져온 이름을 사용하라.

- 적절한 '프로그래머 용어'가 없다면 문제 영역에서 이름을 가져온다. 


### 의미 있는 맥락을 추가하라.

- 어느 메서드가 state라는 변수 하나만 사용한다면?
- addr라는 접두어를 추가해 addrFirstName, addrLastName, addrState라 쓰면 맥락이 좀더 분명해진다.


### 불필요한 맥락을 없애라

- 모든 클래스 이름을 GSD로 시작하겠다는 생각은 전혀 바람직하지 못하다.
- 이름에 불필요한 맥락을 추가하지 않도록 주의한다.
- 일반적으로는 짧은 이름이 긴 이름보다 좋다. 단, 의미가 분명한 경우에 한해서다.
