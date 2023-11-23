## Java의 데이터 표현
- `int`와 `long`이 나누어지는 이유
- 변수 선언은 특정한 byte에 변수가 들어갈 공간을 확보하는 것  
  > `int`의 자료형은 4byte가 확보됨  
  > bit로는 총 32bit  
  > 한 개의 비트는 0 또는 1의 값을 보관 가능

  ### 정수 부호 표현
  1. 절대값을 2진수로 표현함
  ```Java
  -14 -> 14 -> 0000 1110
  ```
  2. 남는 비트를 0으로 채움
  ```Java
  1110 -> 0000 1110
  ```
  3. 각 비트가 0이면 1, 1이면 0으로 변환
  ```Java
  0000 1110 -> 1111 0001
  ```
  4. 1을 더함
  ```Java
  1111 0001 -> 1111 0010
  ```

### 실수 부동 소숫점
- 실수 데이터 저장 방식

1. 숫자를 2진수로 변환함
```Java
10.25 -> 1010.01
```
2. 이후 정수가 한 자리만 남도록 비트를 이동하고, 이동한 만큼 2의 거듭제급을 곱한 형태로 표현
```Java
1.01001 * 2 ^ 3 // 정규화 과정
```
 
 3. 지수에 `Bias`를 더함
 ```java
 3 + (2 ^ 8 - 1) -> 3 + 127 -> 130 -> 10000010 (지수부)
 ```
 4. 부호를 부호 비트에, 지수를 지수부에, 남은 유효 숫자는 가수부에 저장함
 ```Java
 (부호)  (지수)       (가수)
0    - 1000 0010 - 010 0100 0000 0000 0000 0000
/// 남는 공간에는 0을 채워 넣음
 ```