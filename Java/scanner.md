 ## 데이터 입력 받기
 - Scanner를 이용하여 사용자의 데이터를 입력 받을 수 있다.

 ```Java
 Scanner scanner = new Scanner(System.in);
System.out.println(scanner.nextLine());
 ```
 - `Scanner`를 사용하려면 자료형(`int`, `String`)처럼 선언 및 할당을 한다.
 -  한 줄의 입력을 문자열 데이터로 해석하여 할당할 때에 사용함 (`scanner.nextLine()`)
---
 ### Scanner 사용시 유의할 점
 - `Scanner`는 줄 단위로 입력을 받지 않고 `공백` 문자를 기준으로 동작한다.
 ```Java
 byte scanByte = scanner.nextByte();
short scanShort = scanner.nextShort();
```
  - 상기 코드는 한 줄에 네 개의 숫자를 입력할 경우 동시에 작동한다.
  - `nextLine()`의 경우 다음 개행(즉, 입력 key인 Enter)까지를 반환한다.

***여러 줄의 값을 할당받아 출력할 때에는 `next()`를 활용***

---
### 다양한 자료형의 데이터 입력 받기
```Java
byte scanByte = scanner.nextByte();
short scanShort = scanner.nextShort();
int scanInt = scanner.nextInt();
long scanLong = scanner.nextLong();
float scanFloat = scanner.nextFloat();
double scanDouble = scanner.nextDouble();
boolean scanBool = scanner.nextBoolean();
```
> 자료형에 따라 변경되는 명령어를 확인할 수 있음

***`float`, `long`의 경우 변수 선언처럼 `F`, `L`을 추가하지 않음***


