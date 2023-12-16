## 변수와 자료형

### 변수(Variable)
- 데이터를 담는 상자와 같은 역할
- 일정 값을 저장, 정보를 담아두는 것
- 변할 수 있는 수

```Java
public class HelloJava {
    public static void main(String[] args) {
        int a = 100; // a -> 변수!
        System.out.println(a);
        String b = "Hello, Variable!"
        System.out.println(b);
    }
}
```
 
```
100
Hello, Variable!
```

> `System.out.println()`은 괄호 안에 있는 값을 출력하는 코드  
> `int a = 100;, String b = "Hello, Variable!"`로 변수를 선언
 - 변수는 `<자료형> <이름> = <값>`의 형태로 만들 수 있음
 - 선언된 변수의 값은 재할당 등의 변경이 가능하나 **자료형의 형태는 변경이 불가능함**
 ```Java
 int date; // date라는 int형 변수를 선언
date = 100; // date 변수에 100이라는 값을 할당 -> 변수 초기화
```
> 위처럼 1) 변수를 먼저 선언하고 2) 값을 할당할 수 있음

```Java
int month = 11, day = 20;
```
> 한 줄에 여러 개의 변수를 동시에 선언할 수 있음
- 현 시점에서 사용하는 변수는 지역 변수이다
- 지역 변수는 초기화를 해야 컴파일이 가능하다

<details>
<summary>
  변수 <이름> 설정 규칙 (Naming Convention)
</summary>

  1. 숫자로 시작 불가능 (`1st`, `2nd` 등)   
   2. `_`와 `&`외의 특수문자 사용 불가능  
   3. `int`, `class`, `retrun` 등의 예약어 사용 불가능 (Java 내부적으로 사용하는 단어
   )  
> ***camelCase로 통용하여 식별자 설정하기***
</details>

---

### 자료형(Type)
> 변수를 선언하면서 어떤 형식의 데이터를 저장할지 정의할 때에 사용함

1. 논리형
 - `boolean` : `true`와 `false`를 값으로 저장  
 > 조건식, 논리형 계산식에 사용
 2. 문자형
  - `char` : 문자를 저장
  > 한 개의 문자만을 저장할 수 있음
  3. 정수형
- `int` - 정수형 데이터를 저장 ***4byte***
- `long` - 큰 정수형 데이터를 저장 ***8byte***
- `byte` - 이진법의 데이터를 저장 ***1byte***
- `short` - c언어 호환용 데이터
> 주로 `int`와 `long`을 사용
4. 실수형
- `double` - 64비트(8바이트)까지의 실수
- `float` - 32비트(4바이트)까지의 실수 
5. 문자열의 표현
- `String` - 문자로 이루어진 문자열을 저장할 수 있음
```Java
int intNumber = 10; //정수
double realNumber = 365.25; //실수
char character = 'a'; //문자
boolean trueOrFalse = true;//참, 거짓
String string = "this is string"; //문자열
```

---

### 기본형과 참조형
 #### 기본형
- `int`, `long`, `double`, `boolean`처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입
#### 참조형
- 배열과 같이 데이터에 접근하기 위한 참조(주소값)를 저장하는 데이터 타입
- 객체와 클래스를 담을 수 있는 변수들도 모두 참조형
>기본형은 자요형에 따라 사이즈가 명확하게 설정되어 있음  
> 참조형은 동적으로 사이즈 변경이 가능하다

 ***기본형 변수에는 실제 값이 들어있지만, 참조형 변수에는 위치(참조값)이 들어있다.***
 ```
  객체는 `.(dot)`을 통해, 배열은 `[]`을 통해 메모리상에 생성된 객체를 찾아가야 사용이 가능하다
  ```

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
- 참조형: 메서드로 참조형 데이터를 전달하면, 참조값이 복사되어 잔달된다.  
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




