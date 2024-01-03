## IoC Container
- 제어 반전을 구현하기 위해 Spring Framework에서 사용하는 것


### Inversion of Control(제어 반전)
- Spring Boot는 내부적으로 요청을 받는 부분이 만들어져 있는 상태
- 개발자는 어떤 요청을 받았을 때 어떤 행동을 할지만 정해주면 되는 형태

### Bean
 - IoC Container의 관리를 받는 객체
 - 어떤 클래스를 Bean으로 정의하면, 해당 클래스를 필요로 하는 상황에 활용함
 - 이를 Dependecy Injection(의존성 주입)이라고 칭함