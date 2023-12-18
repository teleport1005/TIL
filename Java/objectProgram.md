## 객체 지향 프로그래밍
- 프로그래밍 방식은 크게 `절차 지향 프로그래밍`과 `객체 지향 프로그래밍`으로 나뉜다

### 절차 지향 프로그래밍
- 실행 순서를 중요하게 생각하는 방식
- 흐름을 순차적으로 따르며 처리한다
- `어떻게`를 중심으로 프로그래밍

### 객체 지향 프로그래밍
- 객체를 중요하게 생각하는 방식
- 객체들 간의 상호작용을 중심으로 프로그래밍
- `무엇을`을 중심으로 프로그래밍

>`절차 지향`은 데이터와 데이터에 대한 처리 방식이 분리되어 있다  
>`객체 지향`은 데이터와 메서드가 하나의 객체 안에 포함되어 있다

### 속성과 기능
- 모든 데이터를 단순하게 추상화한다면 속성(데이터)와 기능으로 분류할 수 있다
1. 자동차  
  속성: 차량 색상, 현재 속도, 브랜드, 차량 이름  
  기능: 엑셀, 브레이크, 시동 걸기, 문 열기   
2. 동물  
  속성: 크기, 체온, 이름, 먹이  
  기능: 먹기, 걷기, 뛰기, 자기
  ---

### 캡슐화
- `속성` 데이터와 `메서드` 기능을 `Class`에서 하나의 단위로 묶어서 활용한다

```Java
public class MusicPlayer {
    int volume = 0;
    boolean isOn = false; // 속성

    void on() {
        isOn = true;
        System.out.println("음악 플레이어를 시작합니다");
    } // 기능
    void off() {
        isOn = false;
        System.out.println("음악 플레이어를 종료합니다");
    } // 기능
```
  ### 캡슐화의 접근 제어
  - 데이터와 데이터를 처리하는 메서드를 묶어서 접근을 제한할 수 있다 
  1. 데이터: 객체의 데이터에 직접 접근할 수 없도록 제어한다.  
           메서드를 통하여 접근하도록 한다.  
           >접근을 제어하지 않으면 캡슐화가 깨진다
  2. 기능: 내부에서만 사용하는 기능들은 접근할 수 없도록 제어한다.  
>데이터는 모두 숨기고, 꼭 필요한 기능만 노출하는 것이 좋은 캡슐화



### 생성자
- 객체를 생성함과 동시에 기능을 수행시킬 수 있게 함
1. 생성자 작성
```Java
public class MemberConsturct {
    String name;
    int age;
    int grade;

    // 생성자 부분
    MemberConsturct(String name, int age, int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}
```
>생성자는 `Class` 이름과 같게 생성하며 반환 타입이 없다
>생성자를 직접 정의하게 되면 반드시 호출값이 필요하다
```Java
public class ConsturctMain1 {
    public static void main(String[] args) {
        MemberConsturct member1 = new MemberConsturct(); 
        // 컴파일 오류 발생        
    }
}
```
2. 생성자 호출
```Java
public class ConsturctMain1 {
    public static void main(String[] args) {
        MemberConsturct member1 = new MemberConsturct("user1", 16, 90); // 생성자를 통해서 선언
    }
}
```
>생성자는 인스턴스를 생성하고 나면 즉시 호출된다  
>`new` 명령어 다음에 생성자 이름과 매개변수에 맞추어 인수를 전달하면 된다

- 호출을 생성자를 이용하여 한 번에 처리가 가능하다
- 생성자 호출을 누락시킨 상태로 시스템이 작동하는 것을 방지한다

3. 기본 생성자  
 - `Class`에 생성자가 없으면 `Java`는 기본 생성자를 만든다.
 - 만들어진 생성자가 한 개라도 있다면, 기본 생성자는 만들어지지 않는다.

>생성자도 메서드 오버로딩처럼 사용이 가능하다

---

### 접근 제어자
- `private`: 모든 외부 호출을 막는다.  
  클래스 안에서 속성과 기능을 숨긴다.
- `default`: 같은 패키지 내에서의 호출은 허용한다. (기본값)  
  패키지 안에서 속성과 기능을 숨긴다.
- `protected`: 같은 패키지 내에서의 호출을 허용하면서 패키지가 달라도 상속 관계의 호출은 허용한다.  
  상속 관계로 속성과 기능을 숨긴다.
- `public`: 모든 외부 호출을 허용한다.

>허용 범위 순서  
`private` -> `default` -> `protected` -> `public`

  ### 접근 제어자의 사용
  - 접근 제어자는 필드와 메서드, 생성자에 사용된다.
  - 클래스 레벨의 접근 제어자는 `public`과 `default`만 사용이 가능하다
  - `public` 클래스는 파일명과 같은 이름으로 생성되어야 한다
    - 하나의 자바 파일에 `public`클래스는 하나만 등장할 수 있다
    - `default` 파일은 무한정 생성 가능

  ### Getter & Setter
  - `private` 으로 설정된 속성등에 접근하기 위해 public 메서드를 만들어 속성의 값을 반환하게 만들 수 있다.
  ```Java
  public class Car {
    private String name;
    private String brand;

    //Getter 메서드
    public String getName() {
        return name;
    }

    public String getBrand() {
        return brand;
    }
}
  ```
  ```Java 
  Car someCar = new Car(); 
  System.out.println(someCar.getBrand());
  System.out.println(someCar.getName());
  ```
  - 단순 접근이 아닌  Setter 메서드로 자유롭게 값을 변경하게 할 수도 있다
  ```Java
   public void setFuel(int fuel) { //Setter 메서드
        this.fuel = fuel;
    }
  ```

  ### Wrapper Class
  - int, char, boolean과 같은 자료형은 클래스가 아닌 원시타입이다. 이들을 객체지향적 관점에서 활용할 수 있도록 해주는 클래스를 Wrapper Class라 부른다.
  - 다양한 기능들이 내장되어 있다.

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



### 상속
- 클래스를 상속받아 만들어진 기능을 재활용하여 확장
- 속성과 기능을 공유
- 독자적인 동작 구현, 확장성 증진
- `has-a` 형식으로 클래스의 코드를 상속하여 활용
- `extends <클래스명>`

### 다형성
- 서로 다른 객체가 하나의 공통된 클래스 형태로 취급
- 메서드 오버로딩
>같은 이름의 메서드로 여러 기능 활용
- 메서드 오버라이딩 `@Override`
>같은 메서드가 어떤 객체가 사용하느냐에 따라 기능 변경
```
서브 클래스에서 변경하고 싶은 슈퍼 클래스와 동일한 이름의 메서드를 만들면 `오버라이딩`이 가능
```

### 추상화
- 실제 기능이 만들어지지 않은 추상 클래스를 바탕으로 기능을 위임
- 개별적 기능을 분리
- `interface` 키워드를 사용하여 기능 구현 인터페이스 정의 가능

## Object 클래스
- Java의 모든 클래스는 Object를 상속받는다.
