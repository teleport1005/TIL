## 배열(Array) 
- 하나의 변수에 여러 데이터를 저장하기 위해 주로 활용한다.
---
- 변수 선언시 자료형 뒤에 `[]`를 덧붙이면 만들어진다.
- 그 뒤 `{}`를 이용하여 복수의 값을 대입할 수 있다.
- 저장된 데이터는 `<변수명>[]`을 사용하여 가져울 수 있다.  
***`[]`안의 순서는 `0`부터 시작한다***
```Java
int[] scores = {85, 75, 90};
scores[1] = 80;

System.out.println(scores[0]);
System.out.println(scores[1]);
System.out.println(scores[2]);
```
- 배열의 값이 정해지기 전이라면 크기를 먼저 설정할 수 있다.
```Java
String[] names = new String[4];
names[0] = "alex";
System.out.println(names[0]);
