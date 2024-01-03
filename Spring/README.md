## Spring이란?
- 대표적인 Web Framework

### 클라이언트 - 서버 구조
- Web 환경에서 전송하는 역할을 하는 컴퓨터와 응답하는 역할을 하는 컴퓨터가 데이터를 주고받는 형태로 작동하는 형태를 말한다


### Web
- World Wide Web
- 컴퓨터를 통해 공유된 Web, 거미줄 처럼 엮인 공간

### URL
- Uniform Resource Locator
- 어떤 컴퓨터의 어디에 어떤 자원이 있는지를 표현하기 위한 문자열
```Assembly
https://www.google.com/search?q=techit
<scheme>://<authority>/<path>?<query>#<anchor>
```
1. `scheme` - 어떤 규약을 가지고 요청을 해야 하는지,
2. `authority` - 어디에 있는 컴퓨터(프로세스)인지,
3. `path` - 그 컴퓨터(프로세스) 내부에 어디에 있는지,
4. `query` - 그 자원에 대한 추가 조건 등
>컴퓨터를 구분하기 위한 부분은 authority 는 기본적으로 Spring Boot가 실행되어 있는 컴퓨터를 의미  

### Framework의 역할
- 반복적으로 행해야 하는 작업을 미리 구현해서 모아놓은 것