## Java Practice Challenges 
- Java 변수와 자료형, 데이터 입력 받기를 활용한 예제 풀기

1. 사용자에게 입력을 받고, 동일한 내용을 세번 출력하는 코드를 작성하시오.
```Java
Scanner scanthr = new Scanner(System.in);
        System.out.print("아무 내용이나 입력해 주시면 세 번 반복하겠습니다.");
        String thrTime = scanthr.nextLine();
        System.out.println(String.format("%s %s %s", thrTime, thrTime, thrTime));
```
```
아무 내용이나 입력해 주시면 세 번 반복하겠습니다.챗 GPT 짱이다!
챗 GPT 짱이다! 챗 GPT 짱이다! 챗 GPT 짱이다!
```
2. 두 개의 숫자를 입력 받고, 순서를 바꿔서 출력하시오.
```Java
Scanner scannerset = new Scanner(System.in);
        System.out.print("첫 번째 숫자를 입력해 주세요.");
        int oneNum = scannerset.nextInt();
        System.out.print("두 번째 숫자를 입력해 주세요.");
        int twoNum = scannerset.nextInt();
        System.out.println(String.format("%d %d", twoNum, oneNum));
```
```첫 번째 숫자를 입력해 주세요.89
두 번째 숫자를 입력해 주세요.25
25 89
```
3.   아래 모양을 출력하는 코드를 만들어 보시오.
```
        *   *  
       *** ***  
      *********  
      *********  
        *****  
          *
``` 
```Java
        System.out.println("  *  *  ");
        System.out.println(" *** *** ");
        System.out.println("*********");
        System.out.println("*********");
        System.out.println("  *****  ");
        System.out.println("    *    ");
```
4. 시간과 오전, 오후를 입력받고 ex 오전 xx시의 형식으로 출력하는 코드를 작성하시오.
```java
        Scanner scanner = new Scanner(System.in);
        System.out.print("오전, 오후를 입력해 주세요: ");
        String day = scanner.nextLine();
        System.out.print("시간을 숫자로 입력해 주세요: ");
        int time = scanner.nextInt();
        System.out.println(String.format("%s %d시", day, time));
```
```
오전, 오후를 입력해 주세요: 오전
시간을 숫자로 입력해 주세요: 11
오전 11시
```
5. 사용자에게 3개의 0.0 ~ 4.5 사이의 실수를 입력 받고, 3명의 이름을 입력받은 뒤,  
  이름 - <이름>, 학점 - <실수>의 형태로 3 줄을 출력하는 프로그램을 작성하시오.  
  ```Java
        Scanner scannerscore = new Scanner(System.in);
        System.out.println("학점 세 개를 순서대로 입력해 주세요.");
        double scoreA = scannerscore.nextDouble();
        double scoreB = scannerscore.nextDouble();
        double scoreC = scannerscore.nextDouble();
        System.out.println("이름을 순서대로 입력해 주세요.");
        String[] name = new String[3];
        name[0] = scannerscore.next();
        name[1] = scannerscore.next();
        name[2] = scannerscore.next();
        System.out.println(String.format("이름 - %s, 학점 - %.2f", name[0], scoreA));
        System.out.println(String.format("이름 - %s, 학점 - %.2f", name[1], scoreB));
        System.out.println(String.format("이름 - %s, 학점 - %.2f", name[2], scoreC));
  ```
  ```
  학점 세 개를 순서대로 입력해 주세요.2.26
3.45
1.02
이름을 순서대로 입력해 주세요.
김중간
김과탑
김학고
이름 - 김중간, 학점 - 2.26
이름 - 김과탑, 학점 - 3.45
이름 - 김학고, 학점 - 1.02
  ```
6. 사용자로부터 두 개의 숫자를 입력받아 더한 값을 출력하는 프로그램을 작성하시오.

```Java
        Scanner scannercomputer = new Scanner(System.in);
        System.out.println("첫 번째 숫자를 입력하세요.");
        int numberA = scannercomputer.nextInt();
        System.out.println("두 번째 숫자를 입력하세요.");
        int numberB = scannercomputer.nextInt();
        System.out.println(numberA + numberB);
```
```
첫 번째 숫자를 입력하세요.8850
두 번째 숫자를 입력하세요.9542
18392
```

> 배워가는 점
> - `%`는 문자열 포맷팅(String.format)을 위해 사용됨.(***`""`빼먹지 말자..)  
> - `String.format()` 메서드는 주어진 형식에 따라 `값`을 `문자열`로 변환한다.

---


