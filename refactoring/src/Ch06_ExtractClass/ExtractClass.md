# :book: 자바로 배우는 리팩토링 입문 

--------------------------------------

## :pushpin: 클래스 추출 (Extract Class)

> 클래스는 각각 정해진 일이 있어서 그 일을 완수할 책임이 있다.

- '클래스 하나에 책임 하나'가 이상적이지만, 개발하다보면 클래스 몸집이 늘어서 한 클래스가 여러 책임을 지는 경우도 꽤 있다.

- 기존 클래스가 지는 책임 중에 누군가에게 넘길 수 있는 것이 있는지 찾아본다. 

- 그러고 나서 책임을 넘길 새로운 클래스를 만든다.

    - 구체적으로는 기존 클래스에서 **필드**와 **메서드**를 추출해서 새로운 클래스로 옮긴다.

- **클래스 추출**을 하면 방대한 클래스가 작아져서 클래스가 해야 할 원래 책임이 명확해진다.


### :seedling: 클래스 추출

이름 | 클래스 추출(Extract Class)
---- | ---- |
상황 | 클래스를 작성함
문제 | 한 클래스가 너무 많은 책임을 지고 있음
해법 | 묶을 수 있는 필드와 메서드를 찾아 새로운 클래스로 추출
결과 | O 클래스가 작아짐 <br/> O 클래스의 책임이 명확해짐 <br/> X 클래스 개수가 늘어남


#### 방법 

1. 새로운 클래스 작성
    - (1) 클래스의 책임을 어떻게 추출할지 결정
    - (2) 추출한 책임을 담당할 새로운 클래스 작성. 기존 클래스의 책임이 이름과 일치하지 않게되면 기존 클래스의 이름을 바꿈
    - (3) 기존 클래스에서 새로운 클래스로 링크 작성 <br /> 반대 방향 링크는 가능한 한 만들지 않음 (링크는 단방향)

2. 필드 이동
    - (1) 기존 클래스에서 새로운 클래스로 필요한 필드 이동 
    - (2) 이동할 때마다 컴파일해서 테스트
3. 메서드 이동
    - (1) 기존 클래스에서 새로운 클래스로 필요한 메서드 이동
    - (2) 이동할 때마다 컴파일해서 테스트
4. 추출한 클래스 검토
    - (1) 클래스 인터페이스(API)를 줄일 수 있는가
    - (2) 새로운 클래스를 외부에 공개해야 하는가
    (3) 공개한다면 외부에서 수정 가능하게 할 것인가
    
    
#### 관련 항목

- 클래스명 변경 : 클래스를 추출한 결과로 클래스명이 책임과 일치하지 않으면 이름을 변경함
- 필드 이동 : 기존 클래스에서 새로운 클래스로 필드를 이동함
- 메서드 이동: 기존 클래스에서 새로운 클래스로 메서드를 이동함 


````
public class Book {
    private String _title;
    private String _isbn;
    private String _price;
    private String _authorName;
    private String _authMail;
    ...
}
````

:bulb: 클래스 추출을 위한 필드 이동

````
public class Book {
    private String _title;
    private String _isbn;
    private String _price;
    private Author _author;
}
````

````
class Author {
    private String _name;
    private String _mail;
}
````

:bulb: 클래스 추출을 위한 메서드 이동 

```
public class Book {
    private String _authorName;
    
    public String getAuthorName() {
        return _authorName;
    }
}
```

:bulb: 클래스 추출을 위한 메서드 이동 / 기존 클래스에서 새로운 클래스로 위임

```
public class Book {
    private Author _author;
    
    public String getAuthorName() {
        return _author.getName();
    }
}

```

```
private String _name;
    
   public String getName() {
       return _name;
}
```

- 위임(delegation)이란 '맡긴다'는 뜻
- '기존 클래스에서 새로운 클래스로 위임'은 '기존 클래스에서 새로운 클래스의 메서드를 호출해서 처리하게 만든다'는 의미

