## Spring Beans
 ### Beans -> IoC Container가 관리하는 객체 (Singleton Pattern)
- Spring Framwork는 IoC Container와 Dependency Injection으로 클래스가 유연하게 역할 분담을 할 수 있도록 도움을 준다.
- Spring은 클래스가 Bean 객체로 등록될 수 있도록 다양한 어노테이션을 제공한다
> `org.springframework.stereotype` 패키지 내부에 있는 Spring Stereotype Annotation의 종류와 활용 용도 알기

  ### `@Component`
   - 가장 기초가 되는 어노테이션
   - 기타 어노테이션을 활용하기 어려울 때 사용할 수 있음

  ### `@Service`
   - 비즈니스 로직을 담당하는 어노테이션
   - 프로젝트의 서비스가 실제로 무슨 일을 하는지 나타내기 위한 용도

  ### `@Controller` 
   - 사용자의 입력을 처리하기 위한 부분을 나타냄
   - `@RequestMapping`과 주로 활용하여 인터페이스를 구현

  ### `@Repository`
   - 데이터베이스와 직접적으로 소통하는 요소를 지칭하는 어노테이션
   - `MyBatis`, `JDBC`, `JPA` 등 어떤 데이터베이스를 사용하든 동일

  ### `@Configuration` & `@Bean`
   - 프로젝트 내부에서 활용하기 위한 설정 모음
   
    
    