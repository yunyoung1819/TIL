## 6장. 객체와 자료구조

### 자료 추상화 

예제 6-1과 예제 6-2에서 차이를 살펴보자. 두 클래스 모두 2차원 점을 표현한다.
그런데 한 클래스는 구현을 외부로 노출하고 다른 클래스는 구현을 완전히 숨긴다.

- 예제 6-1. 구체적인 Point 클래스

````
public class Point {
    public double x;
    public double y;
}
````

- 예제 6-2. 추상적인 Point 클래스

````
public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
````

- 예제 6-1은 구현을 노출한다. 
- 변수를 private으로 선언하더라도 각 값마다 조회(get) 함수와 설정(set)함수를 제공한다면 
구현을 외부로 노출하는 셈이다.
- 변수 사이에 함수라는 계층을 넣는다고 구현이 저절로 감춰지지는 않는다. 
- 구현을 감추려면 추상화가 필요하다.
- 추상 인터페이스를 제공해 사용자가 구현을 모른 채 자료의 핵심을 조작할 수 있어야 진정한 의미의 클래스다.


- 예제 6-3. 구체적인 Vehicle 클래스

````
public interface Vehicle {
    double getFuelTankCapacityInGallons();
    double getGallonsOfGasoline();
}
````

- 예제 6-4. 추상적인 Vehicle 클래스

````
public interface Vehicle {
    double getPercentFuelRemaining();
}
````

- 6-3은 자동차 연료 상태를 구체적인 숫자 값으로 알려준다.
- 6-4는 자동차 연료 상태를 백분율이라는 추상적인 개념으로 알려준다.
- 6-3은 두 함수가 변수값을 읽어 반환할 뿐이라는 사실이 거의 확실히다. 6-4는 정보가 어디서 오는지 전혀 드러나지 않는다.
- 6-1과 6-2에서는 6-2가, 6-3과 6-4에서는 6-4가 더 좋다.
- 자료를 세세하게 공개하기보다는 추상적인 개념으로 표현하는 편이 좋다.
- 인터페이스나 조회/설정 함수만으로는 추상화가 이뤄지지 않는다.
- 개발자는 객체가 포함하는 자료를 표현할 가장 좋은 방법을 심각하게 고민해야 한다.
- 아무 생각없이 조회/설정 함수를 추가하는 방법이 가장 나쁘다.