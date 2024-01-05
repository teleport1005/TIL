## Spring MVC CRUD
```
Create
Read All
Read One
Update
Delete
```

## CREATE
  ### DTO
  - 데이터 형태 정의
  - Data Transfer Object
  - DTO 객체는 통신을 통해 오가는 데이터를 나타낸다
  ```Java
  public class StudentDto {
    private Long id; // Datebase의 PK
    private String name;
    private String email;
  }
  ```
  ### HTML
  - 사용자의 입력을 받는 input 요소 생성
  ```HTML
  <!-- 사용자가 데이터를 입력할 수 있는 창구 -->
<h1>Create Student</h1>
<!-- 사용자의 데이터를 받기 위한 form -->
<form action="create" method="post"> <!-- form에 액션을 추가하여 create 객체 사용 -->
    <!-- 이름을 입력하기 위한 input -->
    <label for="name-input">
        Name: <input id="name-input" name="name">  <!-- name 속성값을 controller에서 사용-->
    </label><br>
    <!-- 이메일을 입력하기 위한 input -->
    <label for="email-input">
        Email: <input id="email-input" name="email"> <!-- name 속성값을 controller에서 사용-->
    </label><br>
    <!-- 제출 버튼 -->
    <input type="submit">
  ```
  ### Controller
  - 사용자에게 입력을 받고 데이터 변환을 수행

  ```Java
  @Controller
  pubilc class StudentController{
    // /create-view로 요청이 왔을 때 creat.html을 반환하는 메서드
    @GetMapping("/create-view")
    public String creatView() {
      return "create";
    }
    // /create로 이름과 이메일 데이터를 보내는 요청을 받는 메서드
    @PostMapping("/create")
    public String create(
      @RequestParam("name") String name,
      @RequestParam("email") String email
    ) {
      return "create";
    }
  }
  ```
  - HTML 파일 form에 액션을 추가하여 사용

  ### Service
  - 데이터를 받는 Dto를 생성하고 반환하는 역할
  - Controller에 의존성 주입
  ```Java
  //Controller
      private StudentService service;

    public StudentController(StudentService studentService) {
        this.service = studentService;
    }
    // 의존성 주입
  ```

  ### Post/Redirect/Get
  - Double Post Problem을 해소하는 패턴
   1. 사용자가 데이터를 전송(POST)했을 때 
   2. 다른 URL로 이동하게끔하여(Redirect)
   3. 브라우저의 마지막 요청을 GET으로 변경한다

   ```Java
  // /create로 이름과 이메일 데이터를 보내는 요청을 받는 메서드
    @PostMapping("/create")
    public String create(
            @RequestParam("name")
            String name,
            @RequestParam("email")
            String email
    ) {
        service.createStudent(name, email);
        return "redirect:/home"; // redirect 추가
    }
   ```


## READ ALL
  ### Service와 home.html
  - `Service`에 모든 학생을 반환하는 메서드 추가
  ```Java
    // 현재 등록된 모든 학생을 반환한다
    public List<StudentDto> readStudentAll() {
        return studentList;
    }
  ```

  - 리스트를 보여줄 html에 th:if/unless를 사용하여 작성
  ```html
  <h1>Student List</h1>
<!-- 학생이 없을 경우 -->
<div th:if="${studentList.isEmpty()}">
    <p>등록된 학생이 없습니다.</p>
</div>
<!-- 학생이 있을 경우 -->
<div th:unless="${studentList.isEmpty()}" th:each="student: ${studentList}">
    <p>번호: [[${student.id}]]</p>
    <p>이름: [[${student.name}]]</p>
    <p>이메일: [[${student.email}]]</p>
</div>
<a href="/create-view">Create</a> <!-- 생성 페이지로 이동하는 링크 삽입 -->
  ```

  - `Controller`에 리스트 반환 메서드 추가
  ```Java
      // home으로 요청으로 받으면 home.html에 studentList를 포함하여 반환하는 메서드
    @GetMapping("/home")
    public String home(Model model) {
        model.addAttribute("studentList", service.readStudentAll());
        return "home";
    }
  ```
  >💡 HTML에서 링크 / 리다이렉트 정리 필요

## READ ONE
  ### Service.readOne, read.html
  - Service에서 하나의 id(PK)를 기준으로 Dto(데이터)를 반환하게끔 작성
  ```Java
      public StudentDto readStudent(Long id) {
        // studentList의 데이터를 하나씩 확인해서 getId가 id인 데이터 반환
        for (StudentDto studentDto: studentList) {
            if (studentDto.getId().equals(id)) {
                return studentDto;
            }
        }
        // 없을 경우 null 반환
        return null;
    }
  ```

  - HTML 작성 / model에서 student를 받았다고 가정
  ```html
<body>
<!-- 학생 번호(id)와 이름 -->
<h1>[[${student.id}]]. [[${student.name}]]</h1>
<!-- 학생의 이메일 -->
<p>이메일: [[${student.email}]]</p>
<!-- 홈으로 가는 링크 -->
<a href="/home">Back</a>
  ```

  - `Controller`에 read.one 메서드 추가
  ```Java
      @GetMapping("/{id}")
    public String readOne(@PathVariable("id") Long id, Model model) {
        StudentDto dto = service.readStudent(id);
        model.addAttribute("student", dto);
        return "read";
    }
  ```
  > 💡 `@PathVariable`을 사용하여 id를 할당하자

## UPDATE
> 💡 대상 데이터를 가져온 후(READ), 새로운 데이터를 제공하는 것(CREATE)

  ### update.html과 Controller.updateView
  - update.html은 create.html과 거의 동일하게 작성된다
  ```html
<title>Update</title>
</head>
<body>
<!-- 데이터 갱신 대상 정보 -->
<h1>Update: [[${student.id}]]. [[${student.name}]]</h1>
<form th:action="@{/update/{id}(id=${student.id})}" method="post">
    <!-- 원본의 데이터를 기본값으로 설정해 줘야 한다 -->
    <label for="name-input">
        Name: <input id="name-input" name="name" th:value="${student.name}">
    </label><br>
    <label for="email-input"> 
        Email: <input id="email-input" name="email" th:value="${student.email}">
    </label><br>
    <!-- 제출 버튼 -->
    <input type="submit">
  ```

  - Service에서 갱신 메서드 작성
  ```Java
      public StudentDto updateStudent(Long id, String name, String email) {
        for (StudentDto studentDto : studentList) {
            if (studentDto.getId().equals(id)) {
                studentDto.setName(name);
                studentDto.setEmail(email);
                return studentDto;
            }
        }
        return null;
    }
  ```
  > 💡 id(PK)를 기반으로 바꿀 데이터를 정하고 set으로 갱신

  - Controller에서 UPDATE 수행 메서드 작성
  ```Java
      @PostMapping("/update/{id}")
    public String update(
            @PathVariable("id") Long id,
            @RequestParam("name") String name,
            @RequestParam("email") String email
    ) {
        StudentDto dto = service.updateStudent(id, name, email);
        return String.format("redirect:/read/%s", dto.getId());
    }
  ```

## DELETE
  ### delete.html과 Controller.deleteView
  - 삭제 확인 용 form 작성 
  ```html
<!-- 삭제하기 버튼 -->
<form th:action="@{/delete/{id}(id=${student.id})}" method="post">
    <input type="submit" value="Delete">
</form>
  ```
   > 💡 `readOne` 페이지에서 수정, 삭제가 이루어지나 페이지 추가 가능

  - `Service`에서 삭제 기능 메서드 작성 
  ```Java
      // id를 바탕으로 학생을 제거하는 메서드
    public void deleteStudent(Long id) {
        // 몇 번째 원소를 제거하면 되는지
        int target = -1;
        // 리스트의 각 원소를 확인하면서 주어진 id와 일치하는 원소가 있으면
        // 그 index를 저장
        for (int i = 0; i < studentList.size(); i++) {
            if (studentList.get(i).getId().equals(id)) {
                target = i;
                break;
            }
        }
        // 그 index의 위치에 있는 데이터를 studentList에서 제거
        if (target != -1) {
            studentList.remove(target);
        }
    }
  ```
  > 💡 `Stream`과 `StudentDao`를 활용하여 리팩토링이 가능하다


  - `Controller`에서 삭제 구현 메서드 작성
  ```Java
    @PostMapping("/delete/{id}")
    public String delete(@PathVariable("id") Long id) {
        service.deleteStudent(id);
        return "redirect:/home"; // 삭제 후 홈으로 리다이렉트
    }
  ```




