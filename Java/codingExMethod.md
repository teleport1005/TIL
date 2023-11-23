## Java Practice Challenges 

1. 미세먼지 수치를 입력받고,  
0 ~ 30 이면 "좋음"  
31 ~ 80 이면 "보통"  
80 ~ 150 이면 "나쁨"  
151 ~ 이면 "매우 나쁨" 이라는 문자열을 반환하는 메서드를 작성하시오.
```Java
import java.util.Scanner;

public class d3Q6methods {
    public static String dustPrint(int n) {
        if (n <= 30) {
            return "좋음";
        } else if (n <= 80) {
            return "보통";
        } else if (n <= 150) {
            return "나쁨";
        } else {
            return "매우 나쁨";
        }
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("미세먼지 수치를 입력해 보세요.");
        int dustNow = scanner.nextInt();
        String result = dustPrint(dustNow);
        System.out.println("현재 미세먼지 수치는 " + result + "입니다.");
    }
}
```
```
미세먼지 수치를 입력해 보세요.
23
현재 미세먼지 수치는 좋음입니다.
```
---
2. 지금은 오전 7시다. 정수 n을 인자로 받아, n 시간 후 시계의 시침이 어떤 숫자 위에 있는지를 반환하는 메서드를 작성하시오.
(단, 입력이 0 <= n <= 127 를 벗어나면 -1을 반환하시오.)
```Java
import java.util.Scanner;

public class d3Q7methods {
    public static int timeA (int n) {
        int timeNow = 7;
        if (n < 0 || n > 127) {
            return -1;
        } else {
            return (timeNow + n) % 12;

        }
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("현재 시간은 7시입니다. 몇 시간 뒤를 확인하고 싶으신가요?");
        int time = scanner.nextInt();

        System.out.println(time + "시간 뒤에는 " + timeA(time) + "시에 시침이 옵니다.");
    }
}
```
```
현재 시간은 7시입니다. 몇 시간 뒤를 확인하고 싶으신가요?
9
9시간 뒤에는 4시에 시침이 옵니다.
```
---
3. 사칙연산을 나타내는 문자(char) (+, -, *, /) 하나와
두 개의 정수를 입력받아, 각 기호에 대응하는 연산의 결과를 반환하는 메서드를 작성하시오.
```Java
public class d3Q8methods {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("숫자를 입력하세요.");
        int a = scanner.nextInt();
        char operator = '+';
        System.out.println("계산하고 싶은 숫자를 입력하세요.");
        int b = scanner.nextInt();

        System.out.println(a + " + " + b + " 는 " + operation(operator, a, b)+ "입니다.");
    }
    public static int operation(char operator, int a, int b) {
        int result = 0;
        if (operator == '+') {
            result = a + b;
        } else if (operator == '-') {
            result = a - b;
        } else if (operator == '*') {
            result = a * b;
        } else if (operator == '/') {
                result = a / b;
        }
        return result;
    }
}
```
```
숫자를 입력하세요.
322
계산하고 싶은 숫자를 입력하세요.
12
322 + 12 는 334입니다.
```