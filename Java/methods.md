## 메서드 (methods)
- 클래스 내부에서 특정 기능을 하는 코드를 모아 실행할 수 있게 해 주는 코드의 묶음
 > 일반적인 프로그래밍 언어에서의 함수 역할 수행  
 >```System.out.println(), scanner.nextLine(), String.format()```도 메서드
```Java
public class D4methods {
    public static void main(String[] args) {
        System.out.println("main 메서드");
    }
}
```
```Java
    // main 메서드
    public static void main(String[] args){
        System.out.println("main도 메서드!");
        System.out.println(addTwoInt(10,20));
    }
    // 두 개의 정수를 더하는 메서드
    public static int addTwoInt(int a, int b){ // < 메서드 호출
        return a + b; // = 30
```
---
### 메서드 선언
 ```Java
 public static int add(int a, int b)
 ```
 - public : 다른 클래스에서 호출할 수 있는 메서드 (!= private)
 - static : 객체를 생성하지 않고 호출할 수 있는 정적 메서드
 - int :  반환 타입 정의
 - add : 메서드 이름 정의, 호출할 때 사용
 - (int a, int b) : 전달하는 입력값, 파라미터(매개변수)
 ---

 ### 메서드 본문
 ```Java
 int sum = a + b;
 return sum;
 ```
 >메서드의 실행 결과를 반환하려면 `return`문을 사용해야 함
 ---

 ### 메서드 호출
 ```Java
 int sum1 add(5, 10);
 int sum2 add(15, 20);
 ```
 >`add` 메서드를 호출하여 파라미터(매개변수) 값 대입  
 
***Java는 항상 변수의 값을 복사해서 대입한다***
 ---

 ### 메서드 호출과 용어 정리

 ```java
 호출: call("hello", 20)
 메서드: int call(String str, int age)
 ```
 #### 인수(Argument)
 - `hello`, `20`처럼 넘기는 값을 인수라고 함
#### 매개변수(Parameter)
- 메서드를 정의할 때 선언한 변수인 `String str`, `int age`를 매개변수, 파라미터라고 함
>메서드를 호출할 때 인수를 넘기면 해당 인수가 매개변수에 대입된다

---

### 메서드의 정의
```java
public static int add(int a, int b) {
 //메서드 본문, 실행 코드
}
제어자 반환타입 메서드이름(매개변수 목록) {
 메서드 본문
}
```
- 제어자:  public , static 과 같은 부분
- 반환 타입: 메서드가 실행된 후 반환하는 데이터의 타입 지정  
 -> 만약 없다면 `void`를 사용한다.
 - 메서드 이름: 메서드를 호출하는 데에 사용되는 이름
 - 매개변수: 입력 값으로 메서드 내부에서 사용되는 변수.  
 -> 만약 없다면 지정하지 않아도 된다. `add()`처럼 비워둠
 메서드 본문: 실제 메서드가 실행할 코드를 작성한다  
---

```Java
public static int addTwoInt(int a, int b) //(int a, int b) <매개변수
```
> 매개변수의 자료형은 대부분 사용 가능함

### 반환(Return)
- 메서드의 결과값을 돌려주는 것
- ***메서드는 반환을 해 주어야 동작함***
- ***return*** 키워드를 사용
- return문을 만나면 바로 메서드를 빠져나간다
- 반환과 출력은 다름
```
scanner.nextLine()
>입력을 읽고 문자열을 반환

System.out.println()
>출력을 하고 반환하지 않음
```

### 재귀 함수
- 계승(factorial)
- n부터 1까지의 자연수를 모두 곱한 수
```
f(n) = n x (n-1) x (n-2) x ... 2 x 1 -> `n!`
f(n) = n x f(n-1)
```
- 가독성과 편의성을 위해 코딩에 사용
```Java
    public static int factorial(int n){
        if (n == 1 || n == 0) {
            return 1;
        } else {
            return n * (factorial(n - 1));
        }
    }
```

### 메서드 오버 로딩(Method Overloading)
- 같은 이름의 다른 매개변수 형태의 메서드를 생성할 수 있음
- 호출시 활용도가 높아진다
```Java
    public static int add(int a, int b){
        return a + b;
    }
    public static long add(long a, long b){
        return a + b;
    }

    public static long add(int a, long b){
        return a + b;
    }
```

### 가변 인자 (Varargs)
- `String.format()`과 같이 인자의 갯수 변동이 있을 때에 활용 가능한 기능
```Java
public static String format(String format, Object... args) {
    return new Formatter().format(format, args).toString();
}
```
> 매개변수 자료형 뒤에 `...`을 추가하여 배열처럼 활용