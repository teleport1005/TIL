## 문자열 응용
 - 문자열 데이터는 `"`를 이용하여 표현

 ```Java
 System.out.println("Hello, World!");
 ```
 ```
 Hello, World!
 ```
 ---
 - 문자열로 `"`를 표현하고 싶을 때 사용할 수 있는 방법
 ```java
System.out.println("\"See you tommorow!\" he said.");
 ```
 ```
 "See you tommorow!" he said.
 ```
 > `\`(Escape Sequence)를 이용하여 `"` 표현 가능

---
- 다양한 데이터 표현의 예시
```Java
System.out.println("개행문자: \n 이 다음은 아래줄에 표현됩니다.");
System.out.println("탭키: \t다음 탭의 위치까지 옮긴 뒤 표현됩니다.");
System.out.println("Carriage Return: \r줄의 앞으로 옮깁니다.");
System.out.println("백스페이스: \b앞의 문자를 하나 지웁니다.");
```
```
개행문자: 
 이 다음은 아래줄에 표현됩니다.
탭키: 	다음 탭의 위치까지 옮긴 뒤 표현됩니다.
줄의 앞으로 옮깁니다.
백스페이스:앞의 문자를 하나 지웁니다.
```
> 개행문자는 `Enter키` 입력과 같음
---
### 문자열 서식 설정 String Formatting
 - String Formatting은 변수를 `String`에 저장하여 응용할 수 있다.
 ```Java
int dust = 10; /// `dust`에 `int` 정수 값을 저장
String status = "좋음"; /// `status`에 `String` 문자열 값을 저

System.out.println(String.format("미세먼지 농도: %d (%s)", dust, status));
```
```
미세먼지 농도: 10 (좋음)
```
> 대치하고 싶은 부분을 `%`로 시작하는 포맷 코드를 추가하여 작성  
> `,`로 구분하여 대입 데이터를 차례로 입력

| 코드 | 자료형 |
| --- | --- |
| %s | 문자열(String) |
| %c | 문자(char) |
| %d | 정수(int) |
| %f | 부동소수(float, double) |

**`format`은 여러 변수를 문자열에 삽입할 때 응용하면 좋다.**
>`print`는 줄바꿈을 하지 않고 출력한다.
>`println`은 출력 후 줄바꿈을 실행한다.



