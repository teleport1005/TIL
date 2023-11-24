## 객체와 Class(클래스)
- 객체 지향 프로그래밍
>각 객체들이 필요한 역할을 담당하여 작동할 수 있도록 하는 프로그래밍
### 객체란?
- 정보를 담아 실체하고 작동하는 것
> 실제의 데이터
### 클래스란?
- 객체에 정보와 기능을 담는 것
>정보, 기능, 설계도, 틀
---
```
각각 개별적인 하나의 자동차 = 객체
모든 자동차의 개념 - 클래스
```
```Java
public static void main(String[] args) {
    Car myCar = new Car();
    String myStr = "new string object";
}
```
> `Car`는 클래스, `myCar`는 `Car`의 인스턴스인 객체이다.
### 속성(attribute)
 - 하나의 객체가 가질 수 있는 성질 또는 데이터
 ```Java
public class Car {
    public String name;
    public String brand;
    public int fuel;
}
```
> 객체의 데이터를 클래스 내부에서 정의할 수 있다.
```Java
public static void main(String[] args) {
    Car myCar1 = new Car();
    // 속성에 `.`을 이용해 접근하고,
    // 변수에 데이터를 할당하듯
    // 속성에 데이터를 할당할 수 있다.
    myCar1.name = "K5";
    myCar1.brand = "Kia";
    myCar1.fuel = 72;
    // 값을 가져올때도 `.`을 통해 가져온다.
    System.out.println(
        String.format("My car name is: %s", myCar1.name));
```

-----
- public class '   '
- Java 파일 하나에 하나의 클래스 정보 입력
```Java
public class Main{
  public static void main(String[] args){
    System.out.println("Hello, World!");
  }
}
```
> Java 기능 수행을 위한 코드를 class 내부에 작성해야 한다

### 정적 제어자
- `static` 키워드로 클래스의 메서드나 속성에 붙여 정적 메서드, 정적 변수를 생성할 수 있다.

### 접근 제어자
- `public` > 클래스 정보를 변경 가능
- `private` > 객체 내부에서만 접근 가능

### Getter와 Setter 메서드
- 객체가 가진 속성을 가져오거나 설정할 수 있는 메서드
- `get` 또는 `set`과 변수 이름으로 생성

### 생성자(Constructor)
- 객체를 생성할 때 호출
```Java
public class Car {
    private String name;
    private String brand;
    private int fuel;
    public Car(String name, String brand, int fuel) {
        this.name = name;
        this.brand = brand;
        this.fuel = fuel;
    }
}
```
```java
Car someCar = new Car("K5", "Kia", 72);
System.out.println(someCar.getName());
System.out.println(someCar.getBrand());
someCar.setFuel(72);
System.out.println(someCar.getFuel());
```
> `new` 키워드로 활용이 가능하다.
