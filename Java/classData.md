## Java의 데이터 저장
- class의 객체, 변수의 저장

### Stack Memory
- 변수가 저장될 공간을 `Stack Memory`에 할당하여 호출
- 메서드 종료시 사라진다

### Heap Space, 객체와 주소
- 클래스와 같은 객체들은 `Heap Space`에 할당됨
- 메서드가 종료되어도 객체의 데이터를 저장함

### 유용한 메서드들

| 메서드 | 기능 |
| --- | --- |
| Integer.parseInt(String s) | 문자열이 나타내는 정수를 반환한다. |
| Double.parseDouble(String s) | 문자열이 나타내는 실수를 반환한다. |
| Character.isDigit(char ch) | 문자가 숫자를 나타내는지 확인한다. |
| Character.isLetter(char ch) | 문자가 글자를 나타내는지 확인한다. |
| string.length() | 문자열의 글자수를 반환한다. |
| string.substring(int beginIndex) | 문자열을 beginIndex 부터 자른 문자열을 반환한다. |
| string.charAt(int index) | 문자열의 index 위치의 char를 반환한다. |
| string.indexOf(String str) | 주어진 문자열이 시작하는 index를 반환한다. |
| string.split(String regex) | 주어진 정규표현식을 기준으로 문자열을 나눠 배열로 반환한다. |