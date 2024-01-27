## File handling
- 서버와 클라이언트간 오가는 `file` 정보 다루기

### 정적 파일(Static)
- 사용자에게 변환 없이 전달되는 파일
- CSS, Image, 영상, HTML 등
- Spring Boot `resources/static`에 파일을 저장하면 정적 파일 전달 가능
- applicartion 설정 변경하여 경로 변경 가능
```yaml
spring:
  mvc:
    # 어떤 경로에서 정적 파일 응답을 할지를 결정하는 설정
    static-path-pattern: /static/**
  web:
    resources:
      # 어떤 폴더의 파일을 정적 응답으로 전달할지 설정
      static-locations: file:media/,classpath:/static
```

### Multipart
- `@RequestParam`으로 `MultipartFile` 인자 받기

```Java
@PostMapping(
  value = "/multipart",
  consumes = MediaType.MULTIPART_FORM_DATA_VALUE //multipart/form-data 요청 받기
)
public String multipart(
    @RequestParam("name") String name,
    // 받아주는 자료형을 MultipartFile
    @RequestParam("file") MultipartFile multipartFile
    ) 
```
- 파일을 저장할 경로 생성 및 저장
```Java
// 파일을 저장할 경로 + 파일명 지정
Path downloadPath = Path.of("media/" + multipartFile.getOriginalFilename());
// 저장
multipartFile.transferTo(downloadPath);
```
>✏ `media` 폴더 안에 file 저장


>✏ [사용자 프로필 이미지 업로드 기능 만들기](userAvatar.md)


