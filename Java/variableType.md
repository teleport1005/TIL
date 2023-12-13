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
---

### 기본형과 참조형
 #### 기본형
- `int`, `long`, `double`, `boolean`처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입
#### 참조형
- 배열과 같이 데이터에 접근하기 위한 참조(주소값)를 저장하는 데이터 타입
- 객체와 클래스를 담을 수 있는 변수들도 모두 참조형
>기본형은 자요형에 따라 사이즈가 명확하게 설정되어 있음  
> 참조형은 동적으로 사이즈 변경이 가능하다

```Java
int intNumber = 10; //정수
double realNumber = 365.25; //실수
char character = 'a'; //문자
boolean trueOrFalse = true;//참, 거짓
String string = "this is string"; //문자열
```




