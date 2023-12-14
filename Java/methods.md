## 메서드 (methods)
- 클래스 내부에서 특정 기능을 하는 코드를 모아 실행할 수 있게 해 주는 코드의 묶음  

***변수 명은 일반적으로 명사를 사용하나 메서드는 동작을 수행하기 때문에 동사를 주로 사용한다***
### 메서드 사용의 장점
1. **코드 재사용**: 특정 기능을 캡슐화하여 호출로써 코드의 재사용이 가능하다
2. **코드의 가독성**: 이름(수행하는 목적의 동사명)이 부여되기 때문에 작업이 명확하여 가독성이 좋다
3. **모듈성**: 큰 프로그램을 나누어 작은 부분으로 관리할 수 있다 = 디버깅이 쉽다
4. **코드 유지 관리**: 수정이나 업데이트시 해당 메서드만 수정하기에 변경 사항 적용이 편하다
5. **재사용성과 확장성**: 다른 프로그램이나 프로젝트에도 사용이 가능하며 새로운 기능 추가, 확장이 유용하다
6. **추상화**: 메서드를 사용하는 곳에서는 자세한 구현을 알지 못해도 사용할 수 있다 = 분업에 용이하다
7. **테스트와 디버깅 용이성**: 독립적으로 테스트하고 디버그할 수 있다. 버그 찾기에 유용하다.
---


 > 일반적인 프로그래밍 언어에서의 ***함수*** 역할 수행  
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
    add(int a, int b)
    add(long a, long b)
    add(int a, long b)
```
>같은 이름의 메서드를 여러 개 정의하는 것
```Java
    int add(int a, int b)
    double add(int a, int b) // 컴파일 오류 발생
```
>매개변수의 타입이나 순서가 다를 때만 오버로딩이 가능하다  

>타입에 맞는 메서드를 찾아서 먼저 실행되고, 형 변환 가능한 타입을 실행한다

### 가변 인자 (Varargs)
- `String.format()`과 같이 인자의 갯수 변동이 있을 때에 활용 가능한 기능
```Java
public static String format(String format, Object... args) {
    return new Formatter().format(format, args).toString();
}
```
> 매개변수 자료형 뒤에 `...`을 추가하여 배열처럼 활용