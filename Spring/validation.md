## Spring Boot에서 다양한 예외 처리 방법
  ### ResponseStatusException
  - 가장 간단한 예외 처리 방법
  - `throw new ResponseStatusException();`을 발생시킬 수 있음
  - 간편하게 활용 가능하나 동일한 코드를 여러 번 반복해야 한다
  ```Java
  public UserDto updateUser(Long id, UserDto dto) {
    Optional<User> optionalUser
            = repository.findById(id);
    if (optionalUser.isEmpty())
        throw new ResponseStatusException(HttpStatus.NOT_FOUND);
    ...
  ```

  ### @ExceptionHandler
  - `@ExceptionHandler` 어노테이션을 `Controller`에 추가하여 활용
  - 전달받은 예외를 바탕으로 사용자에게 전달할 응답을 조절하기 쉬움
  ```Java
  @ExceptionHandler(IllegalArgumentException.class)
  public ResponseEntity<ErrorResponseDto> handleIllegalArgument(
        final IllegalArgumentException exception) {
    return ResponseEntity
            .badRequest()
            .body(new ErrorResponseDto(exception.getMessage()));
  }
  ```

  ### @ControllerAdvice & @RestControllerAdvice 
  - 위 `@ExceptionHandler` 어노테이션은 하나의 Controller 단위에서만 활용 가능
  - 전체 프로젝트에 전달되는 예외를 정리할 수 있음
  ```Java
  @RestControllerAdvice
  public class UserControllerAdvice {
    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<ErrorResponseDto> handleIllegalArgument(
            final IllegalArgumentException exception) {
        return ResponseEntity
                .badRequest()
                .body(new ErrorResponseDto(exception.getMessage()));
    }
  }
  ```

  ### 커스텀 예외 활용
  - 큰 프로젝트에서 일관성 있는 에외 처리를 위해 커스터마이징할 수 있다
  - 상속 관계를 활용하여 간소화
  ```Java
  // 400 응답을 발생시키기 위한 부모 추상 예외
  public abstract class Status400Exception extends RuntimeException{
    public Status400Exception(String message) {
        super(message);
    }
  }

  public class InvalidEmailException extends Status400Exception {
    public InvalidEmailException() {
        super("email format invalid");
    }
  }

  public class ConflictException extends Status400Exception {
    public ConflictException() {
        super("username not unique");
    }
  }
  ```
  - `@ExceptionHandler`로 관리할 수 있음
  ```Java
  @ExceptionHandler(Status400Exception.class)
  @ResponseStatus(HttpStatus.BAD_REQUEST)
  public ErrorResponseDto handle400(
        final Status400Exception exception) {
    return new ErrorResponseDto(exception.getMessage());
  }
  ```

--- 


## Validation (유효성 검사)
- 사용자가 입력한 데이터를 검증(유효성 검증)
- `HTML`단에서도 입력 데이터 검증이 가능하나, 사용자가 변경하기 쉬운 프론트단에서 제약하는 것이므로 백단에서도 검증 처리 필요
```gradle
implementation 'org.springframework.boot:spring-boot-starter-validation'
```
- 의존성 추가
- `Jakarta Bean Valdiation`이 유효성 검증을 위한 기술을 명시한다
- `Hibernate Validator`가 실제로 유효성 검증을 하는 프레임워크

 ### @Valid
 - 기본적인 유효성 검증 진행
 - `DTO`에서 어노테이션을 활용하여 해당 DTO 데이터가 지켜야 할 규칙 설정
 - 이후 `@Valid` 어노테이션으로 그 규칙을 지키는지 확인
 ```Java
 public class UserDto {
    private Long id;
    // 사용자가 입력하는 데이터 중 검증하고 싶은 데이터
    @NotNull
    private String Username;
 }
 ```
 ```Java
 @PostMapping("/validate-dto")
  public String validateDto(
  @Valid // 이 데이터는 입력을 검증해야 한다
  @RequestBody
  UserDto dto
  ) {
     return "done";
    }
 ```
  #### 사용 가능한 규칙 설정 어노테이션
  >✏ https://beanvalidation.org/2.0/spec/#builtinconstraints(공식 문서)
  - `AssertTrue` , `AssertFalse` : `boolean`, `Boolean` 의 참 거짓
  - `Min`, `Max`, `DecimalMin`, `DecimalMax`, `Negative`, `Postive` … : 숫자형 자료형의 최대 최소 등
  - `Past`, `Future` : 시간 관련
  - `@NotNull` : 데이터가 `null` 이 아님을 검증
  - `@NotEmpty` : 데이터가 비어있지 않음을 검증 
  - `@NotBlank` : 문자열에 대하여, 공백이 아님을 검증

 ### @Validated
 - `@Valid` 어노테이션과는 약간 다른 방식으로 동작
  #### 메서드 파라미터의 개별 검증
   - `@RequestParam` 이나 `@PathVariable`을 검증할 때 사용
   ```Java
   @Validated
  @RestController
  public class UserController {
    /...
    // @Validated가 붙은 클래스의 메서드 파라미터는 검증이 가능하다.
    @GetMapping("/validate-params")
    public String validateParams(
            @Min(14)
            @RequestParam("age")
            Integer age
    ) {
        return "done";
    }
  }  
   ```

