## Java Practice Challenges 
- Java 연산자를 활용한 연습 문제 풀기

1. 어떤 야구단의 승, 무승부, 패를 입력받고, 아래와 같이 출력하시오.
> 00승 0무 0패 승률: 0.000 (소숫점 세 번째 자리까지)

```java
        Scanner scanner = new Scanner(System.in);
        System.out.println("구단의 승, 무승부, 패를 순서대로 입력해 주세요.");
        System.out.print("승 수:");
        int win = scanner.nextInt();
        System.out.print("무승부 수:");
        int draws = scanner.nextInt();
        System.out.print("패 수:");
        int lose = scanner.nextInt();

        double winnetPersent = (double) win / (win + lose);
        System.out.print(win + "승 " + draws + "무 " + lose + "패 ");
        System.out.printf(("승률: %.3f"), winnetPersent);
```
```
구단의 승, 무승부, 패를 순서대로 입력해 주세요.
승 수:92
무승부 수:2
패 수:43
92승 2무 43패 승률: 0.681
```
---
2. 어떤 수 A와 B를 입력받고 A를 B로 나눈 몫과 나머지를 "A = 몫 * B + 나머지"의 형태로 출력하여라.
```Java
        Scanner scanner = new Scanner(System.in);
        System.out.println("A 값을 입력하세요.");
        int A = scanner.nextInt();
        System.out.println("B 값을 입력하세요.");
        int B = scanner.nextInt();

        int price = A / B;
        int anther = A % B;
        System.out.println("A = " + price + " * B + " + anther);
```
```
A 값을 입력하세요.
32
B 값을 입력하세요.
7
A = 4 * B + 4
```
---
3. ASCII 코드로 'A'는 65이다. 1 ~ 26 사이의 숫자 n이 입력될 때, n번째 알파벳을 대문자로 출력하시오.
```Java
        Scanner scanner = new Scanner(System.in);
        System.out.println("1 ~ 26 사이의 숫자를 입력하시면 해당하는 알파벳을 알려드립니다.");
        int alphabet = scanner.nextInt();
        char number = (char) ('A' + alphabet - 1);
        System.out.println("해당 숫자의 알파벳은 " + number + "입니다.");
```
```
1 ~ 26 사이의 숫자를 입력하시면 해당하는 알파벳을 알려드립니다.
11
해당 숫자의 알파벳은 K입니다.
```
---
4.  정수 A를 입력받아, A^2, A^4, A^8의 1의 자리를 순서대로 한줄씩 출력하시오.
```Java
        Scanner scanner = new Scanner(System.in);
        System.out.println("정수를 입력하세요.");
        int A = scanner.nextInt();

        int aOf2 = (A * A) % 10;
        int aOf4 = (aOf2 * aOf2) % 10;
        int aOf8 = (aOf4 * aOf4) % 10;

        System.out.println(A + "^2의 1의 자리는 " + aOf2);
        System.out.println(A + "^4의 1의 자리는 " + aOf4);
        System.out.println(A + "^8의 1의 자리는 " + aOf8);
```
```
정수를 입력하세요.
82
82^2의 1의 자리는 4
82^4의 1의 자리는 6
82^8의 1의 자리는 6
```
---
5. 체온이 38도 이상이거나 36도 이하일 때에는 병원에 가기로 했다. 
  체온을 입력받아 병원에 가야할지를 `true` 또는 `false`로 출력하여라.

  ```Java
          Scanner scanner = new Scanner(System.in);
        System.out.println("정확한 체온을 입력해 주세요.");
        double temperture = scanner.nextDouble();
        boolean sick = temperture <= 36;
        boolean soSick = temperture >= 38;
        System.out.println(sick || soSick);
  ```
  ```
  정확한 체온을 입력해 주세요.
  38.9
  true
  ```