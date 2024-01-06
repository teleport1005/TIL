## JPA
> 💡 Java는 객체 지향 프로그래밍 언어로 객체간의 상호작용이나 어떠한 객체가 또 다른 객체를 소유함으로써 동작한다.   
> 💡 객체지향적 관점에서 관계형 데이터베이스를 활용하여 객체를 테이블에 매핑하면 실제 SQL문을 작성하지 않기 때문에 의존성이 감소한다. (편리함)
  ### JPA와 Hibernate
  #### JPA – Java Persistence API (Jakarta Persistence)
  - 데이터가 어떻게 테이블에 매핑되는지를 명시한다
  - 인터페이스와 어노테이션으로 구성
  ```Java
  @Entity 
  public class Student {}
  ```
  #### Hibernate
  - JPA 명시를 바탕으로 작동하는 ORM의 프레임워크
  - JPA로 표현된 객체를 실제 데이터베이스에 적용하고 사용한다

  ### JPA 프로젝트 설정
  #### `yaml` 설정
  ```yaml
  spring:
  datasource:
    url: jdbc:sqlite:db.sqlite
    driver-class-name: org.sqlite.JDBC
  jpa:
    hibernate:
      ddl-auto: create
    show-sql: true
    database-platform: org.hibernate.community.dialect.SQLiteDialect
  ```
  - `spring.jpa.hibernate.ddl-auto`: Hibernate가 Entity 객체를 적용하기 위한 DDL을 어떻게 실행할지 정의
  - `spring.jpa.show-sql`: Hibernate에서 실제로 실행한 SQL을 콘솔에서 확인
  - `spring.jpa.database-platform`: Hibernate에서 사용할 SQL Dialect(방언).

  #### `Entity` 작성
  ```Java
  @Data // Lombok
  @Entity
  public class Student {
    @Id // 이 필드가 PK임을 명시
    @GeneratedValue(strategy = GenerationType.IDENTITY) // PK 자동 증가 설정
    private Long id;
    private String name;
    private Integer age;
    private String phone;
    private String email;
    }
  ```
  > 💡 실행하면 database 테이블이 생성된다

  - JPA는 EntityManager를 사용하고, Spring Data JPA는 JpaRepository를 사용한다
  ```Java
  public interface StudentRepository 
      extends JpaRepository<StudentEntity, Long> {
        // 사용할 Entity 클래스와 해당 클래스의 PK 타입
      }
  ```
  ```Java
  @Service
 public class StudentService {
    private final StudentRepository studentRepository;
    /...
 }
  ```
  > 💡 Bean 객체로 등록되기 때문에 의존성 주입이 자동으로 이루어짐

  #### `JpaRepository`로 `CRUD` 만들기

  1. CREATE - 새 객체를 생성한 후 `save()`

 ```Java
  @Service
  public class StudentService {
    private final StudentRepository studentRepository;

    public void createStudent(
      String name,
      Integer age,
      String phone,
      String email
    ) {// 주어진 정보로 새로운 Student 객체를 만든다
        Student student = new Student();
        student.setName(name);
        student.setAge(age);
        student.setPhone(phone);
        student.setEmail(email);
        studentRepository.save(student);
    }
  }
  ```

  2. READ - readAll, readOne  
  - readAll
  ```Java
    public List<Student> readStudentAll() {
    return studentRepository.findAll();
    }
  ```
  - readOne
  ```java
    public Student readStudent(Long id) {
        return studentRepository.findById(id).orElse(null);
    }  
  ```

  3. UPDATE - – Entity 조회하고 수정한 후 `save()`
  ```Java
    public void update(
            // 수정할 데이터의 PK가 무엇인지
            Long id,
            // 수정할 데이터
            String name,
            Integer age,
            String phone,
            String email
    ) {
        // 1. 업데이트할 대상 데이터를 찾고,
        Student target = 
                studentRepository.findById(id).orElse(new Student());        
        // 2. 데이터의 내용을 전달받은 내용으로 갱신하고,
        target.setName(name);
        target.setAge(age);
        target.setPhone(phone);
        target.setEmail(email);
        // 3. repository를 이용하여 저장한다.
        studentRepository.save(target);
    }  
  ```

  4. DELETE - – 삭제하고 싶은 객체 또는 PK 전달
  ```Java
    public void delete(Long id) {
        studentRepository.deleteById(id);
    }  
  ```

  ### ManyToOne & OneToMany
  - 관계형 데이터베이스(RDB)에서는 외래키를 이용하여 표현
  1. **1:1 One to One 관계**  
    - 한 테이블의 레코드 하나가 다른 테이블의 레코드 하나와 연관된 관계  
    - 특정 데이터를 성능 또는 보안적 측면에서 나눌 때 사용
  2. **N:1, Many to One 관계**  
    - 한 테이블의 레코드 0개 이상이 다른 테이블의 레코드 하나와 연관된 관계  
    - 일반적인 데이터베이스의 가장 흔한 관계 (게시글 – 댓글, 가게 – 상품 등)
  3. **M:N, Many to Many 관계**  
    - 한 테이블의 레코드 0개 이상이 다른 테이블의 레코드 0개 이상과 연관된 관계  
    - 양쪽 테이블의 PK를 Foreign Key로 가진 Join Table, Associative Table 활용

  #### JPA에서 관계를 가지는 Entity 만들기
  1. `@ManyToOne`
  ```Java
    // FK Colum -> Join Colum
    @ManyToOne
    private Instructor advisor;  
  ```
  > 💡 `Instructor` 데이터를 `Student` 데이터와 `advisor` KEY로 연결
  - `Controller` create 부분에 연결 키 데이터 연동 추가
  ```Java
    @PostMapping("create")
    public String create(
            @RequestParam("name")
            String name,
            @RequestParam("age")
            Integer age,
            @RequestParam("phone")
            String phone,
            @RequestParam("email")
            String email,
            @RequestParam("advisor-id")
            Long advisorId
    ) {
        studentService.create(name, age, phone, email, advisorId);
        return "redirect:/student";
    }  
  ```
  - `Service` create 부분에 연결 키 데이터 연동 추가
  ```Java
    public void create(
            String name,
            Integer age,
            String phone,
            String email,
            // 지도교수의 PK를 받아온다.
            Long advisorId
    ) {
        // 주어진 정보로 새로운 Student 객체를 만든다
        Student student = new Student();
        student.setName(name);
        student.setAge(age);
        student.setPhone(phone);
        student.setEmail(email);
        // 지도교수를 찾는다
        Optional<Instructor> optionalInstructor
                = instructorRepository.findById(advisorId);
        // 학생의 지도교수를 할당한다
        student.setAdvisor(optionalInstructor.orElse(null));
        // repository의 save 메서드 호출
        studentRepository.save(student);
    }  
  ```
 - `readOne`에서 연관 관계 `Entity` 가져오기 
 ```Java
    @GetMapping("{id}")
    public String readOne(
            @PathVariable("id")
            Long id,
            Model model
    ) {
        Student student = studentRepository.findById(id).orElse(null);       
        model.addAttribute("student", student);
        model.addAttribute("instructor", student.getAdvisor());        
        return "student/read";
    } 
 ```

 2. `@OneToMany`

  - `StudentRepository`에 쿼리 메서드 추가
  ```Java
  public interface StudentRepository extends JpaRepository<Student, Long> {
    List<Student> findAllByAdvisor(Instructor entity);
    List<Student> findAllByAdvisorId(Long id);
  }  
  ```
  > 💡 ID를 사용하거나, Entity 객체를 그대로 활용할 수 있다.

  - Instroctor 클래스에 필드 생성 및 설정
  ```Java
  @Entity
  public class Instructor {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String firstName;
    private String lastName;

    @OneToMany(mappedBy = "advisor")
    private List<Student> advisingStudents;
  }  
  ```














