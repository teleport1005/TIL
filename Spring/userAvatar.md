## User 프로필 이미지 기능 만들기

- 회원가입 후 프로필 사진을 user가 Multipart로 업로드한다고 가정
- 특정 위치에 해당 프로필 사진을 저장한 뒤, 특정 URL로 정적 파일 전송이 가능함
- User 테이블에는 `String`으로 프로필 사진을 추가

```Java
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(unique = true)
    private String username;
    private String email;
    @Setter
    private String phone;
    @Setter
    private String bio;
    @Setter
    private String avatar; // 프로필 사진 image 추가 -> 경로에 요청을 보내야 하기 때문에 String
```

### URL 구성하기
- User 정보 수정 URL
- User 프로필 이미지 업로드 URL 

### 비즈니스 로직 구성
```Java
    // UPDATE USER AVATAR
    // 회원 프로필 사진 변경
    public UserDto updateUserAvatar(Long id, MultipartFile image) {
        // ID로 유저 찾기
        Optional<User> optionalUser = userRepository.findById(id);
        if (optionalUser.isEmpty())
            throw new ResponseStatusException(HttpStatus.NOT_FOUND);

        // 업로드된 파일 저장 위치 결정
        // media/{id}/profile.{확장자}
        // 기존 저장 위치 폴더가 없다면 폴더 만들기
        String profileDir = String.format("media/%d/", id);
        log.info(profileDir);
        // Path를 기준으로 없는 디렉토리 생성
        try {
            Files.createDirectories(Path.of(profileDir));
        } catch (IOException e) {
            // 폴더 만드는 것에 실패하면 log 후 알림
            log.error(e.getMessage());
            throw new ResponseStatusException(HttpStatus.INTERNAL_SERVER_ERROR);
        }
        // 파일 이름에 경로와 확장자를 포함
        String originalFilename = image.getOriginalFilename();
        // whale.png ->  { whale, png }
        String[] filenameSpilt = originalFilename.split("\\.");
        String extension = filenameSpilt[filenameSpilt.length - 1];
        String profileFilename = "profile." + extension;
        log.info(profileFilename);

        String profilePath = profileDir + profileFilename;
        log.info(profilePath);

        // 파일 저장
        try {
            image.transferTo(Path.of(profilePath));
        } catch (IOException e) {
            log.error(e.getMessage());
            throw new ResponseStatusException(HttpStatus.INTERNAL_SERVER_ERROR);
        }

        // User에 업로드 파일 위치 저장
        // http://loaclhost:8080/static/{id}/profile.{확장자}
        String requestPath = String.format("/static/%d/%s", id, profileFilename);
        log.info(requestPath);
        User target = optionalUser.get();
        target.setAvatar(requestPath);

        // 응답
        return UserDto.fromEntity(userRepository.save(target));
```
### Controller 구성
```Java
    @PutMapping("/{userId}/avatar")
    public UserDto avatar(
            @PathVariable("userId")
            Long userId,
            @RequestParam("image")
            MultipartFile imageFile

    ) {
        return userService.updateUserAvatar(userId, imageFile);
    }
```