## 연산자 (Operator)
- 덧셈, 뺄셈, 곱셈, 나눗셈 등의 사칙연산
- 어떠한 연산을 할지 정하는 기호

> 값(혹은 변수): 피연산자 / 부등기호: 연산자

### 산술 연산자
 - `+` 더하기 `-` 빼기 `/` 나누기 `*` 곱하기 `%` 모듈러
- 사칙연산으로 간단한 수학 연산을 하는 연산자  
***`%(모듈러란?)` 왼쪽의 피연산자에서 오른쪽 피연산자로 나눈 나머지를 반환하는 기호.***
```Java
        int plus = 10 + 20; // = 30
        int minus = 20 - 10; // = 10
        int mulitply = 20 * 10; // = 200
        int divide = 20 / 10; // = 2
        int modulo = 15 % 10; // = 5
```
> 사칙연산의 순서와 일치하며 `%` 모듈러도 곱셈과 나눗셈으로 취급한다.

- 변수를 정수로 정의하였는데 값이 유리수로 출력될 때에는 정수까지의 결과값만 도출됨
---
### 형 변환
- 자료형을 적절하게 변경해야 할 때에 쓰임

 > `String` 문자열은 변환이 불가하다.
 - 더 작은 자료형에서 큰 자료형으로 변환은 자동으로 변환이 가능함.(***묵시적 형변환***)  
 ```-> byte -> short -> int -> long -> float -> double```
 - 더 큰 자료형에서 작은 자료형으로 변환할 때에는 수동으로 변환해 주어야 함.
 ```Java
// <자료형> <변수명> = (<자료명>) <변환하려는 값>;
int integer = (int) 2.1;
```  
 > 데이터 손실이 발생하기 때문에 사용에 주의 필요함.
---


### 증감 연산자
 - `++` : 피연산자의 값을 `1` 증가시킴
 - `--` : 피연산자의 값을 `1` 감소시킴
 ```Java
 int a = 10;
 a++; // 11
 a++; // 12
 a--; // 11
 ```
  > 반복 작업에서 반복 횟수로 사용  
  > 배열에서 다음 대상을 나타내는 index
 ```java
  int count = 10;
  System.out.println(++count); // 11 전치계산 -> 출력 전에 1 증가, 값 11
  System.out.println(count++); // 11 후치계산 -> 출력 후에 1 증가, 값 12
  System.out.println(--count); // 11 > 값 12에서 출력 전에 1 감소, 값 11
  System.out.println(count--); // 11 > 값 11에서 출력 후에 1 감소, 값 10
 ```
 > 출력(count) 전에 계산할지, 후에 계산할지 증감 연산자의 위치에 따라 작동함

### 복합 할당 연산자
- 대입, 즉 `=` 할당하는 연산자와 다른 산술 연산자를 합친 연산자
```
 `=` : 왼쪽의 피연산자에 오른쪽 피연산자를 할당
 `+=` : 더한 값을 왼쪽 피연산자에 할당
 `-=` : 뺀 값을 왼쪽 피연산자에 할당
 `*=` : 곱한 값을 왼쪽 피연산자에 할당
 `/=` : 나눈 값을 왼쪽 피연산자에 할당
 `%=` : 나머지 값을 왼쪽 피연산자에게 할당
 ```
 - 변수에 값이 이미 할당된 상태라면 업데이트 형식으로 활용 가능하다.
---


 ### 비교 연산자
- 관계 연산자, boolean 형으로 조건 비교
```
`==` : 왼쪽의 피연산자와 오른쪽 피연산자가 같으면 참(true), 다르면 거짓(false)을 반환  
`!=` : 왼쪽의 피연산자와 오른쪽 피연산자가 다르면 참(true), 다르면 거짓(false)을 반환  
`<` , `>` : 식에서 참이라면 true, 거짓이라면 false를 반환
`<=`, `>=`: 식에서 참이라면 true, 거짓이라면 false를 반환
```
---
### 논리 연산자
- 두 가지 조건(boolean)에 대하여 두 조건의 `true`, `false` 조합에 따라 결과 반환
- 둘 다, 둘 중 하나라도 등  
```Java
&& : 둘 다 true일 경우 true // 하나라도 false일 경우에는 false
 > 그리고, and
|| : 둘 다 false일 경우 false // 하나라도 true일 경우에는 true
 > 그러나, or
 ! : 참이면 거짓, 거짓이면 참을 반환한다 //not
```
 > 복수의 논리 연산자가 조합되어 있다면 ! -> && -> || 순서로 결과 도출
 ---

### 비트 연산자 
- Java의 데이터는 모두 비트로 표현 가능하며 비트의 연산도 가능하다.
``````
 - `AND`
  & : 두 수 각 자리의 비트가 둘다 1이면 결과 자리의 비트도 1 
 - `OR`
  | : 두 수 각 자리의 비트가 둘중 하나라도 1이면 결과 자리의 비트도 1 
 - `XOR`
  ^ : 두 수 각 자리의 비트가 서로 다르면 결과 자리의 비트가 1 (XOR 연산)
 - `NOT`
  ~ : 각 자리의 비트를 1이면 0으로, 0이면 1로 (NOT 연산)
  ``````
 - `SHIFT` 연산
 >LEFT SHIFT, RIGHT SHIFT  
 >`<<` LEFT SHIFT  : 비트를 왼쪽으로 이동  
 >`>>` RIGHT SHIFT : 비트를 오른쪽으로 이동
 
---

 ### 삼항 연산자
 - 하나의 조건이 참인지 거짓인지에 따라 두 가지 값 중 하나를 결정하는 연산자
 ```Java
 int temperature = 37;
 String message = temperature < 38 ? "OK" : "Feverish">
 ```
 > ```boolean ? (true) : (false)```



