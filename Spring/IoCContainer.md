## IoC Container
- 제어 반전을 구현하기 위해 Spring Framework에서 사용하는 것
```
💡 Container란?
- 인스턴스의 생명 주기를 관리
생성된 인스턴스들에게 추가적인 기능 제공
```

### Inversion of Control(제어 반전)
- Spring Boot는 내부적으로 요청을 받는 부분이 만들어져 있는 상태
- 개발자는 어떤 요청을 받았을 때 어떤 행동을 할지만 정해주면 되는 형태

### DI (Dependency Injection)
- 의존성 주입
- 클래스 사이의 의존 관계를 `Bean` 설정 정보를 바탕으로 Container가 자동으로 연결해 주는 것

### Bean
 - IoC Container의 관리를 받는 객체
 - 어떤 클래스를 Bean으로 정의하면, 해당 클래스를 필요로 하는 상황에 활용함
 - 이를 Dependecy Injection(의존성 주입)이라고 칭함
 - `BeanFactory` Container가 이를 생성하고 관리한다

### Component
- `Bean`을 생성하기 위한 애노테이션 중 하나
- 해당 애노테이션을 클래스에 붙이면 `Bean`으로 등록

### Qualifier
- 같은 타입의 `Bean`이 여러 개 있을 경우에 어떤 `Bean`을 사용할지 결정한다

### Autowiring
- 자동으로 `Bean`을 주입해 주는 애노테이션

## DAO란?
-  Data Access Object의 약자로 데이터를 조회하거나 조작하는 기능을 전담하
도록 만든 객체
-  데이터베이스를 조작하는 기능을 전담하는 목적으로 만들어짐
