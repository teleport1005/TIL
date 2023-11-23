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
### 매개변수(Parameter)
- 메서드로 전달될 값들을 정의하기 위해 사용
```Java
public static int addTwoInt(int a, int b) //(int a, int b) <매개변수
```
> 매개변수의 자료형은 대부분 사용 가능함

### 반환(Return)
- 메서드의 결과값을 돌려주는 것
- return 키워드를 사용하여 돌려주고 싶은 결과를 return 뒤에 작성한다
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