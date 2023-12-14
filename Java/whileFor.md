
### 반복문 (while, for, for each)
- 특정 조건(`boolean`)이 `true`일 동안 계속해서 실행되는 명령
- `if`와 일부 비슷하나 반복하며 작동함

1.  `while` 반복문   
  ***반복 횟수가 정해지지 않았을 때 사용***  
  ***조건이 `true`일 동안 반복 실행된다***
  ```java
  while (조건) {
    // 조건이 참일 때 실행되는 코드
}
  ```
```Java
while loan (loan < 0)
>> loan의 값이 0이 될 때까지 반복해서 코드를 반복
```
```Java
        int[] numbers = {2, 3, 5, 6, 19, 23};
        int i = 0;
        // 총합 및 평균 구하기
        int sum = 0;
        while (i < 6) {
            System.out.println(numbers[i]);
            sum += numbers[i];
            i++;
        }
        System.out.println("총 합은 " + sum);
        System.out.println("평균은 " + sum / 6);
```
2. `for` 반복문   
  ***반복 횟수가 정해졌을 때 사용***  
  ***특정 횟수만큼만 반복한다***
  ```Java
  for (초기값; 조건; 증감식) {
    // 조건이 참일 때 실행되는 코드
}
  ```
 - 세 부분으로 나누어 반복할 조건을 설정
 ```Java
 for (int i = 0; i < 10; i++>{
  System.out.println(i);
 })
 ```
 > 변수 선언 (1) 
 > 반복 조건 (2)
 > 반복마다 실행할 코드 설정을 `;`로 구분하여 `()` 안에 작성한다
```Java
// 별 찍기
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < i + 1; j++) {
                System.out.print('*');}
            System.out.println();}
```
3. `foreach` 반복문
- 배열과 같은 복수 데이터의 모음인 변수에 대하여 사용할 수 있음
- 각각의 요소를 탐색한다
``` Java
String[] fruits = {"apple", "pear", "banana"};
for (String name : fruits) {
    System.out.println(name);
}
```
- 배열을 처음부터 끝까지 탐색하며 작동한다
- `:` 오른쪽에 탐색할 변수를 선택하고, 왼쪽에 반복할 때마다 찾은 값을 저장할 변수를 선언한다
- 배열의 값을 하나씩 꺼내서 왼쪽에 있는 변수에 담는 수행 방식이며, 끝에 도달하면 종료된다  

