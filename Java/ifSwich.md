### 조건문 (if, swich)
  1. `if`  
  어떤 조건(boolean)에 대하여 코드를 실행할지 말지 결정하는 제어문
  > 참(`true`)이면 코드를 실행한다
  ```Java
  if (조건) {
    // 조건이 참일 때 실행되는 코드
}
  ```


  ```Java
        Scanner scanner = new Scanner(System.in);
        // 나이를 입력 받고, 20세 미만일 때 입장 불가를 출력해 보자.
        System.out.println("본인의 나이를 숫자로 입력해 주세요.");
        int age = scanner.nextInt();
        if (age < 20) {
            System.out.println("입장 불가");
            System.out.println(String.format("%d년 뒤에 입장이 가능합니다.", 20 - age));
        }
  ```
  ---
  2. `else`  
  if로 지정한 조건 외의 결과들에 대한 실행값을 지정할 수 있음
  >거짓(`false`)이면 코드를 실행한다
  ```Java
  if (조건) {
    // 조건이 참일 때 실행되는 코드
} else {
    // 조건이 거짓일 때 실행되는 코드
}
  ```
```Java
int number = 10;
if (number % 2 == 0) {
    System.out.println("짝수");
}
else { // else의 정의는 if에서 진행됨 -> if가 아니라면,
    System.out.println("홀수");
}
```
---
 3. `else if`
 조건이 여러 개로 나누어질 때에 활용 가능

```Java
// 미세먼지 수치
// 0 ~ 30 : 좋음, 31 ~ 80: 보통, 80 ~ 150: 나쁨, 151 ~ : 매우 나쁨
        int dust = 15;
        if (dust <= 30) {
            System.out.println("좋음");
        } else if (31 <=dust && dust <= 80) {
            System.out.println("보통");
        } else if (81 <= dust && dust <= 150) {
            System.out.println("나쁨");
        } else {
            System.out.println("매우 나쁨");
        }
```
```Java
int zero = 0;
if (zero == 0) {
    System.out.println("is zero");
}
else if (10 % zero == 0) {
    System.out.println("is factor");
}
else {
    System.out.println("not factor");
}
```
> 0을 나누는 코드가 작동될 때에 error가 발생하지만,  
> `if`로 미리 할당을 해 주었기 때문에 해결이 가능  
> **`if` 조건에 맞다면 아래 코드들은 동작하지 않는다**  
---
4.  `switch` - `case`
- 확인해야 하는 조건이 어떤 데이터인지가 중요할 때에 활용
- 변수에 따라 실행될 코드들을 분리할 수 있음
```Java
        String input = "w";
        switch (input){
            case "w":
                System.out.println("up");
                break;
            case "a":
                System.out.println("left");
                break;
            case "s":
                System.out.println("down");
                break;
            case "d":    
                System.out.println("right");
                break; 
            default: // 입력 전 기본 동작 추가 가능
                System.out.println("invalid");
                break; 
        }
```