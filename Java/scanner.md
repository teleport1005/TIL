 ## 데이터 입력 받기
 - Scanner를 이용하여 사용자의 데이터를 입력 받을 수 있다.

 ```Java
 Scanner scanner = new Scanner(System.in);
System.out.println(scanner.nextLine());
 ```
> 한 줄의 입력을 문자열 데이터로 해석하여 할당할 때에 사용 (`scanner.nextLine()`)

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

- `Scanner`는 줄 단위로 동작하지 않으며, 공백 문자를 기준으로 동작
