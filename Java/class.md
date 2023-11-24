## 객체와 Class(클래스)
- 객체 지향 프로그래밍
>각 객체들이 필요한 역할을 담당하여 작동할 수 있도록 하는 프로그래밍
### 객체란?
- 정보를 담아 실체하고 작동하는 것
> 실제의 데이터

### 클래스란?
- 객체에 정보와 기능을 담는 것
>정보, 기능, 설계도, 틀

-----
- public class '   '
- Java 파일 하나에 하나의 클래스 정보 입력
```Java
public class Main{
  public static void main(String[] args){
    System.out.println("Hello, World!");
  }
}
```
> Java 기능 수행을 위한 코드를 class 내부에 작성해야 한다

### 접근 제어자
``````
`public` > 클래스 정보를 변경 가능
`private` > 객체 내부에서만 접근 가능
``````
