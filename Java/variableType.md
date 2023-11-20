## 변수와 자료형

### 변수(Variable)
- 데이터를 담는 상자와 같은 역할
- 일정 값을 저장, 정보를 담아두는 것

```Java
public class HelloJava {
    public static void main(String[] args) {
        int a = 100;
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
 int date;
date = 100;
```
> 위처럼 1) 변수를 먼저 선언하고 2) 값을 할당할 수 있음

```Java
int month = 11, day = 20;
```
> 한 줄에 여러 개의 변수를 동시에 선언할 수 있음

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

- `int` - 정수형 데이터를 저장하는 자료형
- `String` - 문자열 데이터를 저장하는 자료형
- `double` - 실수형 데이터를 저장하는 자료형
- `char` - 글자 데이터를 저장하는 자료형
- `boolean` - 참/거짓 데이터를 저장하는 자료형
- `long` - 큰 정수형 데이터를 저장하는 자료형
```Java
int intNumber = 10; //정수
double realNumber = 365.25; //실수
char character = 'a'; //문자
boolean trueOrFalse = true;//참, 거짓
String string = "this is string"; //문자열
```




