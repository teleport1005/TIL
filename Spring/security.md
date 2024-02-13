# Spring Security (Auth)
- Spring Framework에서 이용할 수 있는 보안 패키지
- 인증과 권한 부여 과정 설계 가능
  - 인증(Authentication): 사용자가 본인을 증명하는 과정
  - 권한(Authorization): 사용자가 어떤 작업을 수행할 수 있는지 결정하는 과정  
  >✏ 상기 인증, 권한 단어를 묶어 `Auth`로 칭한다


![Security](Security.png)  
>✏ Security 추가


  ## Form Login
  - 기본적으로 사용할 수 있는 인증 방식 = Login
  1. 사용자가 로그인 페이지로 이동
  2. 서버가 로그인 페이지로 사용자를 이동시킴
  3. 사용가는 로그인 페이지에서 Id, Password 전달
  3. 서버는 전달된 정보가 일치하는지 확인 후 인증
  >✏ 이후 서버는 쿠키를 이용하여 로그인한 사용자가 누구인지 기억하는 세션을 생성  
  >✏ `쿠키🍪`: 서버에서 사용자의 브라우저로 보내는 `작은 데이터`  
      -> 사용자의 로그인 정보를 쿠키에 담아 저장하여 유지하는 것을 `세션`이라고 부름
      ![cookie](cookie.png)
  >✏ 쿠키가 로그인한 ID 정보를 기억한 상태로 유지하는 것이 세션  
  >✏ Spring security가 세션 관리를 담당할 수 있다    

  ## Login 구현하기
  - `WebSecurityConfig`에서 `filterChain` 메소드 사용
  ### 1. 경로 접근 권한 부여
  ```Java
  @Configuration
  public class WebSecurityConfig {
    @Bean
    // 메서드 결과를 Bean 객체로 관리해 주는 어노테이션
    public SecurityFilterChain securityFilterChain(
      HttpSecurity http
    ) throws Exception {
      http
          .csrf(AbstractHttpConfigurer::disable)
          .authorizeHttpRequests(auth -> auth
            // 어떤 경로에 대한 설정인지 먼저 적용
            .requestMatchers("/no-auth").permitAll()
            // "/no-auth"에는 모두가 접근 가능
            .anyRequest().permitAll() 
            // anyRequest -> 설정한 url 외의 접근에 대해서 기본적으로 허용할 권한 부여 가능
    }
  ```
  >✏ `permitAll`: 모든 사용자 접근 허용  
  >✏ `authenticated`: 인증된 사용자만 접근 허용  
  >✏ `anonymous`: 익명 사용자만 접근 허용 (인증된 사용자는 접근 불가)

  ### 2. Login 설정
   - `UserController` 생성하여 `@Controller` 어노테이션 부여(HTML 응답)
   #### 1) Login Form 컨트롤러 메서드
   ```Java
       @GetMapping("/login")
      public String loginForm() {
        return "login-form";
    }
   ```
   #### 2) Login Form HTML 생성
   #### 3) Login 성공 후 이동할 my-page 컨트롤러 메서드 생성
   ```Java
       @GetMapping("/my-profile")
      public String myProfile(
            Authentication authentication,
            Model model
    ) {
        model.addAttribute("username", authentication.getName());
        log.info(authentication.getName());
        //log.info(((User) authentication.getPrincipal()).getPassword());
        log.info(((CustomUserDetails) authentication.getPrincipal()).getPassword());
        log.info(((CustomUserDetails) authentication.getPrincipal()).getPhone());
        return "my-profile";
    }
   ```
   > ✏ `("/login")` URL 페이지는 `anonymous` 권한 부여 필요  
   > ✏ `("/my-profile")` URL 페이지는 `authenticated` 권한 부여 필요

   #### 4) FilterChain 경로 권한 설정
   - `authorizeHttpRequests` 설정
   - 일종의 Build-Up 패턴으로 동작

   ```Java
    @Bean
    public SecurityFilterChain securityFilterChain(
            HttpSecurity http
    ) throws Exception {
        http
           .csrf(AbstractHttpConfigurer::disable)
           .authorizeHttpRequests(auth -> auth
              // `("/my-profile")` URL 페이지는 `authenticated` 권한 부여
               .requestMatchers("/users/my-profile")
               .authenticated()
              // `("/login")` URL 페이지는 `anonymous` 권한 부여
               .requestMatchers("/users/login")
               .anonymous()
               /...
    }
     return http.build();
   ```

   #### 5) html form 요소를 이용하여 로그인을 할 수 있도록 설정

  ```Java
    .formLogin(formLogin -> formLogin
               // 어떤 경로로 요청을 보내면 해당 로그인 페이지가 나올지 설정
               .loginPage("/users/login") // 매핑 경로 입력
               // 아무 설정 없이 로그인이 성공한 뒤 이동할 페이지
               .defaultSuccessUrl("/users/my-profile")
               // 로그인이 실패시 이동할 페이지
               .failureUrl("/users/login?fail")
    );
  ```
  >✏ `.loginPage()` : 로그인 페이지의 URL을 설정  
  >✏`.defaultSuccessUrl()` : 로그인 성공시의 URL을 설정  
  >✏ `.failureUrl()` : 로그인 실패시의 URL을 설정   
  >✏ `.permitAll()` : 로그인 관련된 URL의 인증 요구사항을 해제

  ### 3. LogOut 설정
  ```Java
    .logout(logout -> logout
          // 어떤 경로로 요청을 보내면 로그아웃이 되는지
          .logoutUrl("/users/logout")
          // 로그아웃 성공시 이동할 페이지
           .logoutSuccessUrl("/users/login")
    );
  ```
  >✏ `.logoutUrl`: 로그아웃을 처리하는 URL을 설정  
  >✏ `.logoutSuccessUrl`: 로그아웃 성공 시 리다이렉트되는 URL을 설정
   - Html form 전달
   ```html
    <form action="/users/logout">
      <input type="submit" value="로그아웃">
    </form>
   ```

  #### 1) 사용자 정보 관리
   - 사용자 정보 관리 클래스 Bean 생성
   - 사용자 정보를 Map 방식으로 저장

  ```Java
    @Bean
    public UserDetailsManager userDetailsManager(
            PasswordEncoder passwordEncoder
    ) {
        // 사용자 1 생성
        UserDetails user1 = User.withUsername("user1")
                .password(passwordEncoder.encode("password1"))
                .build();
        // Spring Security에서 기본으로 제공하는 메모리 기반 사용자 클래스 + 사용자 1
        return new InMemoryUserDetailsManager(user1);
    }
  ```
  #### 2) 비밀번호 암호화
   - `UserDetailsManager`가 비밀번호를 암호화 -> 해독할 때 필요한 Bean 클래스
   - 사용자가 생성한 password를 서비스 제공자도 알지 못하도록 암호화함
  ```Java
    @Bean
    // 비밀번호 암호화 클래스
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
  ```

   >✏ formLogin을 위해서는 `UserDetailsManager`가 필요하며 해당 클래스는 `PasswordEncoder`를 사용  
   >✏ formLogin이 두 클래스를 모두 사용하기 때문에 `@Bean` 객테로 등록 필요함

---



 ### 회원가입 구현
  #### 1. 회원가입 Form Html 작성
   ```html
   <form action="/users/register" method="post">
   ```

  #### 2. URL 접근 권한 설정 (FilterChain 메서드에 URL 권한값 추가)
  ```java
        .authorizeHttpRequests(auth -> auth
           // `("/my-profile")` URL 페이지는 `authenticated` 권한 부여
            .requestMatchers("/users/my-profile", "/users/logout")
            .authenticated()
           // `("/login")`, `()"/users/register")` URL 페이지는 `anonymous` 권한 부여
            .requestMatchers("/users/login", "/users/register")
            .anonymous()
  ```

  #### 3. 회원가입 컨트롤러 메서드 작성
   ```Java
   @GetMapping("/register")
   public String signUpRequest(
        @RequestParam("username") String username,
        @RequestParam("password") String password,
        @RequestParam("password-check") String passwordCheck
  ) {
    // password가 passwordCheck과 일치하면,
    if (password.equals(passwordCheck));  
    // 회원가입 성공 후 로그인 페이지로
    return "redirect:/users/login";
    }
   ```

   > ✏ 앞에서 만들었던 `UserDetailsManager` 와 `PasswordEncoder`를 활용하여 사용자 등록 가능

