## MyBatis
- JDBC를 활용하여 만들어진 framework
- interface 메서드에 SQL을 연결하여 활용
  ### MyBatis 사용 설정
  - `application.yaml`에서 DB 관련 설정 진행
  ```yaml
  spring:
  datasource:
    url: jdbc:sqlite:db.sqlite
    driver-class-name: org.sqlite.JDBC
    # username: sa
    # password: password
  ```
  - `spring.datasource.url`: 데이터베이스에 접속하기 위한 URL
  - `spring.datasource.driver-class-name`: 데이터베이스를 사용할때 사용할 JDBC 드라이버, 사용하는 RDBMS에 따라 다름
  - `spring.datasource.username / password`: 데이터베이스의 접속 정보를 작성하는 곳
  ```yaml
  # MyBatis 사용 설정
  mybatis:
    mapper-locations: "classpath:/mybatis/mappers/*.xml"
    type-aliases-package: "com.example.crud.model"
    configuration:
      map-underscore-to-camel-case: true
  ```
  - `mybatis.mapper-locations`: SQL이 정의된 mapper.xml 파일의 위치 경로 작성
  - `mybatis.type-aliases-package=com.example.mybatis.model`: 위에서 언급한 XML 파일에서 사용할 Java 클래스의 패키지 위치
  - `mybatis.configuration.map-underscore-to-camel-case=true`: snake_case와 camelCase간 자동 변환
  > 💡 `application.yaml`을 사용하는 것이 가독성 면에서 더 뛰어나다

  ### Annotation으로 SQL문 작성
   - `Lombok` `@Data` 활용하여 데이터 생성
  ```Java
  import lombok.Data;
  @Data
  public class Student {
    // 데이터베이스의 PK
    private Long id;
    private String name;
    private String email;
  }
  ```

  - Interface `Mapper` 작성
  - MyBatis는 기본적으로 Interface의 메서드로 SQL 구문 실행
  ```Java
  @Mapper
  public interface StudentMapper {
    @Select("SELECT * FROM student;")
    List<StudentDto> selectStudentAll();
  }
  ```
  > 💡 selectStudentAll() 호출 시 `SELECT * FROM student` 실행  
  > 💡 @Select, @Insert, @Update, @Delete 등을 작성해 줄 수 있다

  - Data Acces Object = DAO 작성
  - 데이터베이스 접근에 대한 관심사 분리 역할
  ```Java
  // 데이터 통신을 담당하는 클래스임을
  // Spring에 알려줌
  @Repository // = Bean으로 등록
  public class StudentDao {
    // MyBatis와 데이터베이스를 연결해주는 객체
    private final SqlSessionFactory sessionFactory;
    // Spring Boot안에 만들어진 SqlSessionFactory Bean이 자동으로 주입
    public StudentDao(SqlSessionFactory sessionFactory) {
        this.sessionFactory = sessionFactory;
    }
  }
  ```
  > 💡 `SqlSessionFactory`: MyBatis가 제공하는 추상화된 JDBC 사용의 기초
  ```Java
      // 데이터베이스에서 학생 데이터를 전부 불러오는 메서드
    public List<Student> readStudentsAll() {
      // SqlSession은 MyBatis와 데이터베이스가 연결되었다는 것을 상징하는 객체
      try (SqlSession session = sessionFactory.openSession()) {
        // Mapper 인터페이스를 가져온다.
        StudentMapper mapper = session.getMapper(StudentMapper.class);
        return mapper.selectStudentAll();
      }
    }
  ```
  > 💡 `SqlSession`: DataBase와의 세션을 나타내는 객체, Mapper interface 제공

  - `Mapper`에 CRUD문 작성
  - Mapper Annotation CRUD (Insert, Select, Update, Delete)
  1. INSERT
  ```java
   @Insert("INSERT INTO student(name, email) " +
    "VALUES(#{name}, #{email});")
    void insertStudent(Student student);
  ```
  2. SELECT
  ```Java
  // Select ONE
    @Select("SELECT * FROM student WHERE id = #{id}")
    Student selectStudent(Long id);
  ```
  3. UPDATE
  ```Java
   @Update("UPDATE student SET " +
     "name = #{name}, " +
     "email = #{email} " +
     "WHERE id = #{id}")
    void updateStudent(Student student);
  ```
  4. DELETE
  ```Java
   @Delete("DELETE FROM student " +
     "WHERE id = #{id}")
    void deleteStudent(Long id);
  ```
  > 💡 `Select` -> `Optional` 활용 가능





