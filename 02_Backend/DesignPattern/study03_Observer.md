# :book: 디자인 패턴
## :pushpin: 옵저버 패턴

### :seedling: Observer pattern
- `관찰자 패턴`은 **변화가 일어 났을 때, 미리 등록된 다른 클래스에 통보해주는 패턴**을 구현한 것이다.
- 많이 보이는 곳은 `event listener`에서 해당 패턴을 사용 하고 있다.

![](images/옵저버패턴.png)

### Sample Code
#### IButtonListener interface
```java
public interface IButtonListener {
    void clickEvent(String event);
}
```

#### Button Class
````java
public class Button {
    private String name;
    private IButtonListener buttonListener;
    
    public BUtton(String name) {
        this.name = name;
    }
    
    public void click(String message) {
        buttonListener.clickEvent(message);
    }
    
    public void addListener(IButtonListener buttonListener) {
        this.buttonListener = buttonListener;
    }
}
````

#### Main Class
````java
public class Main {
    
    public static void main(String[] args) {
        Button button = new Button("버튼");
        
        button.addListener(new IButtonListener() {
           @Override
           public void clickEvent(String event) {
               System.out.println(event);
           } 
        });
        
        button.click("메시지 전달 : click 1");
        button.click("메시지 전달 : click 2");
        button.click("메시지 전달 : click 3");
        button.click("메시지 전달 : click 4");
    }
}
````