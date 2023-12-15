## 객체와 Class(클래스)
- 객체 지향 프로그래밍
>각 객체들이 필요한 역할을 담당하여 작동할 수 있도록 하는 프로그래밍
### 객체란?
- 정보를 담아 실체하고 작동하는 것
> 실제의 데이터, 인스턴스
### 클래스란?
- 객체에 정보와 기능을 담는 것
>정보, 기능, 설계도, 틀
---

### Class의 생성과 사용
#### `Class`의 생성
 ```Java
public class Car {
    public String name;
    public String brand;
    public int fuel;
}
```
- `Car`라는 Class를 정의했다
- `Car Class`에는 이름`name`, 브랜드`brand`, 기름`fuel`의 변수를 가진다
- `Class`에 정의한 변수들은 멤버 변수, 필드`Field`라고 부른다
- 특정 `class`에 소속된 멤버이기 때문에 멤버 변수라 일컫는다
- `Field`는 전통적인 용어로 데이터 항목을 말한다
- `int`가 정수 타입, `String`이 문자 타입인 것처럼 `Car`라는 타입을 생성한 것이다  

---

#### `Class`의 사용
```Java
    Car myCar // myCar라는 Car Class 변수 데이터를 생성
    myCar = new Car(); // myCar에 Class의 참조값을 대입
    myCar.name = "Casper";
    myCar.brand = "Hyundai";
    myCar.fuel = 80;
```
- 멤버 변수에 값을 대입하려면 `.`(dot)을 사용하여 접근한다
- `myCar`에는 `Class`의 데이터 참조값이 있으므로 해당 위치에서 접근하는 것이다
>`Car myCar`라는 변수 선언 부분에서 데이터를 저장하는 메모리 참조값이 생성되고 `myCar.name`은 저장된 메모리의 참조값으로 이동하여 접근, `name`에 데이터를 대입한다

> `Car`는 클래스, `myCar`는 `Car`의 인스턴스인 객체이다.

```
각각 개별적인 하나의 데이터 = 객체
모든 자동차의 개념 - 클래스
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
