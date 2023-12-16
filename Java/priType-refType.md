## 기본형과 참조형

- 기본형(`Primitive Type`): `int` , `long` , `double` , `boolean` 처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입  
- 참조형(`Reference Type`): `Cay myCar`, `int[] students` 와 같이 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터 타입

### 기본형 VS 참조형 - 기본
- 기본형: 숫자 `10`, `20`과 같이 실제 사용하는 값을 담아 바로 사용
- 참조형: 실제 값이 아닌 실제 객체의 위치(참조, 주소)값을 저장  
>참조형에는 객체와 배열이 있다  
객체는 `.(dot)`을 통해, 배열은 `[]`을 통해 메모리상에 생성된 객체를 찾아가야 사용이 가능하다

### 기본형 VS 참조형 - 계산
  - 기본형 변수는 실제 값이 들어있기 때문에 연산이 가능하다
  ```Java
  int a = 10;
  int b = 20;
  int sum = a + b; // 연산 및 출력 가능
  ```
  - 참조형 변수는 실제 값이 아닌 객체의 위치인 참조값이 들어있기 때문에 연산이 불가능하다
  ```Java
  Car myCar = new Car();
  Car yourCar = new Car();
  myCar + yourCar // 오류 발생
  ```
 >상기 계산을 하고 싶다면 `.`을 통해 객체의 멤버 변수에 접근하여 연산할 수 있다
 ```Java
  Car myCar = new Car();
  myCar.fuel = 100;
  Car yourCar = new Car();
  yourCar.fuel = 80;
  int sum = myCar.fuel + yourCar.fuel // 연산 가능
 ```
---

- 기본형 `int`, `long`, `double` 등을 제외한 나머지는 모두 참조형이다
- 기본형은 소문자로 시작한다 Java가 제공하는 데이터 타입이기 때문이다
- 기본형은 개발자가 직접 정의할 수 없다
- 클래스는 대문자로 시작한다
- 클래스는 모두 참조형이다
>`String`은 예외적으로 특별하다  
>클래스이며 참조형이지만 문자 값을 바로 대입할 수 있다 


### 기본형 VS 참조형 - 변수 대입
***Java는 항상 변수의 값을 복사해서 대입한다***
- 기본형: 변수에 값을 대입시 실제 값의 복사본이 대입된다
```Java
int a = 10; // 10
int b = a; // 10
```
>여기에서 `a`의 값을 바꾸더라도 b는 a의 값을 복사하여 대입한 것이기 때문에 b의 값이 같이 바뀌지 않는다


- 참조형: 실제 객체를 대입하는 것이 아닌 객체의 위치를 가르키는 참조값이 복사된다
```Java
Car myCar = new Car();
Car yourCar = myCar;
> 생성한 `myCar`의 객체가 복사되어 전달된 것이 아닌, 이미 메모리에 생성되어 있는 `myCar`의 참조(주소)값만 복사되어 전달된 것이다.
즉, myCar로 가는 방법이 두 변수로 생성된 것이다.
따라서 myCar로 객체의 값을 대입하든, yourCar로 객체의 값을 대입하든 생성되어 있는 메모리 내부의 객체 값이 변경된 것이기 때문에 하나를 바꾸게 되면 같이 바뀌게 된다.
```

### 기본형과 참조형의 메서드 호출
- 기본형: 메서드로 기본형 데이터를 전달하면 해당 값이 복사되어 전달된다  
->메서드 내부에서 파라미터 값을 변경해도 호출차의 변수 값에는 영향이 없다
```Java
    public static void main(String[] args) {
        int a = 10;
        System.out.println("메서드 호출 전 : a = " + a); // = 10
        changePrimitive(a);
        System.out.println("메서드 호출 후 : a = " + a); // = 10
    }

    public static void changePrimitive(int x) {
        x = 20;
    }
```
- 참조형: 메서드로 참조형 데이터를 전달하면, 참조값이 복사되어 전달된다.  
-> 멤버 변수에 도달이 가능해지기 때문에 변경시 호출자의 객체도 변경된다
```Java
    public static void main(String[] args) {
        Data dataA = new Data();
        dataA.value = 10;
        System.out.println("메서드 호출 전: dataA.value = " + dataA.value); // = 10
        changeReference(dataA);
        System.out.println("메서드 호출 후: dataA.value = " + dataA.value); // = 20

    }

    public static void changeReference(Data dataX) {
        dataX.value = 20;
    }
```

---
## 변수와 초기화
### 변수의 종류
- 멤버 변수(필드): `Class`에 선언한 변수
```Java
public class Student {
 String name;
 int age;
 int grade;
}
```
>`name`, `age`, `grade`는 멤버 변수이다.
- 지역 변수: `Method`에 선언한 변수(매개변수도 지역변수이다)
```Java
public class ClassStart3 {
 public static void main(String[] args) {
 Student student1;
 student1 = new Student();
 Student student2 = new Student();
 }
}
```
>`student1`, `student2`는 지역 변수이다.

### 변수의 값 초기화
1. 멤버 변수의 초기화
- 멤버 변수, `Class`에 선언한 변수는 자동으로 초기화된다.
- `int`는 `0`, `boolean`은 `false`, 참조형은 `null`(참조할 대상이 없으므로)로 초기화한다.
- 개발자가 직접 초기화를 할 수도 있다.
```Java
public class InitData {
 int value1; //초기화 하지 않음
 int value2 = 10; //10으로 초기화
}
```
2. 지역 변수의 초기화
- 지역 변수는 해당 메서드에서만 사용하는 변수이다.
- 개발자가 수동으로 값을 지정해 주어야만 한다.
- 초기화하지 않고 사용시 컴파일 오류가 발생한다.
```Java
public static void main(String[] args) {
  int value;
  System.out.println(value); // 오류 발생
```




