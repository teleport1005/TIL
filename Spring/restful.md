# Spring Boot & Rest

## REST
- REpresentational State Transfer
- HTTP를 이용한 서버를 구현할 때 지켜야 하는 설계 원칙
- 서버와 클라이언트 사이의 결합성(의존성) 감소 목적  
  ->성능 향상, 확장성 확보, 사용 편의성 증대

  ### Client - Server Architecture
  - 클라이언트와 서버의 역할 분리
  - 양측의 독립적 발전 추구
  >✏ 서버가 데이터의 표현 방식에 따라 변화하거나, 클라이언트가 데이터의 저장 방식을 알고 사용하지 않게끔 별개로 작동해야 한다

  ### StateLessness
  - 클라이언트가 서버에 보내는 요청에 대해 모두 독립적인 요청으로 사용할 수 있게 설계
  - 서버가 클라이언트의 요청 상태 등을 기억하지 않아도 되도록 설계

  ### Cachevility
  - Cache-Controll Header
  - 캐시 가능성 표현
  >✏ 정적 데이터를 캐시할 것인지에 대한 Cache-Controll Header를 지정해야 한다

  ### Layered System
  - 클라이언트와 서버 요청 도달 과정 분리
  >✏ Load Balancer등으로 부가 서버를 구축하였을 때 클라이언트는 동일 요청만 보내면 되도록 설계해야 한다

  ### Code on Demand (Optional)
  - 실행 가능한 코드 전달로 클라이언트의 기능을 일시적으로 확장
  - `Javascript`와 브라우저 사용

  ### Uniform Interface
  - 일관된 인터페이스 유지 설계로 가장 **근본적인 제약사항**
  - RESTful한 API가 가지는 인터페이스를 묘사함  
    1. 서버 요청 자원을 요청 자체로 구별할 수 있어야 한다 -> URL에 요구 자원 표현 원칙  
    ```
    GET /students/{studentId} //{studentId}인 student 조회 요청이 명확하게 드러남
    ```
    2. 데이터 조작시 데이터의 상태나 표현으로 조작할 수 있도록 설계(`JSON`) -> 관리보다 표현에 중점  
    3. 각 요청과 응답에 충분한 정보를 포함(`Content-Type Header 사용`)
    4. Hypermedia As The Engine Of Application State(HAETOAS) -> 최초의 URL에서 모든 정보를 확인할 수 있게 설계  
    >✏ 실질적으로 구현하기에는 난이도가 높음

## RESTful
- 실질적으로 `REST` 원칙을 모두 지키며 서비스를 개발하는 것은 매우 어려움
- `REST API` 제작하는 것이 아닌 RESTful한 API를 목표로 제작  
- 우선적으로 하기의 원칙을 지키며 API 작업을 진행
  ### 1. URL 구성
  - `URL`이 자원을 논리적으로 표현할 수 있도록 구성하여야 함
  - 할 일 목록 -> `/todo` URL 연결처럼 직관적인 표현

  ### 2. HTTP Method
  - 자원에 적용할 작업을 `HTTP Method`로 구분
  - 추가 -> `POST`, 회수(수정) -> `GET`, 삭제 -> `DELETE`

>✏ 위 원칙들을 지키며 API 작업을 할 경우, Richardson Maturity Model의 Level 2를 달성함  
>✏ 좋은 API 디자인이라고 볼 수 있음




## RESTful한 Article 서비스 만들기

 ### Article & ArticleDto 
 - `Entity` 정의
 
 ### URL 구성
 - `URL` 이름 자체에는 `자원을 식별`한다는 의미를 담고 있다
 - 하나의 `URL`이 자원의 한 종류를 식별할 수 있도록 구성
 - 기본 `URL`은 복수형으로 구성하며, 단일 데이터 요청시에는 id를 포함하여 식별한다
  >✏ `/articles` : 전체 게시글들에 대해서 작업하기 위한 URL  
  >✏ `/articles/{id}` : 어떤 특정 게시글에 대해서 작업하기 위한 URL

 ### Method 기능 정의
 - `URL`로 표현된 자원에 어떤 작업을 할지 `HTTP Method`로 특정짓도록 구성하는 원칙
  >✏ CREATE: 새로운 자원을 생성하기 위한 기능으로, `POST` 사용   
  >✏ READ: 이미 존재하는 자원을 조회하기 위한 기능으로, `GET` 사용   
  >✏ UPDATE: 이미 존재하는 자원을 수정하기 위한 기능으로, `PUT` 사용    
  >✏ DELETE: 삭제하기 위한 기능으로, `DELETE` 사용  

 ### URL과 Method 조합
 - 위 내용을 바탕으로 `URL`과 `Method`를 조합하여 `RequestMapping` 구성
  >✏ 게시글 생성: `POST /articles`  
  >✏ 게시글 전체 조회: `GET /articles`  
  >✏ 게시글 단일 조회: `GET /articles/{id}`  
  >✏ 게시글 수정: `PUT /articles/{id}`  
  >✏ 게시글 삭제: `DELETE /articles/{id}`  

 ### Comment 
 - `comment`는 하나의 `article`에 종속되어 있기 때문에 `URL`에도 참조되어야 한다
  >✏ 게시글에 댓글 추가: `POST /articles/{articleId}/comments`  
  >✏ 게시글 댓글 전체 조회: `GET /articles/{articleId}/comments`  
  >✏ 게시글 댓글 수정: `PUT /articles/{articleId}/comments/{commentId}`  
  >✏ 게시글 댓글 삭제: `DELETE /articles/{articleId}/comments/{commentId}`  

 ### Query Parameter 활용
 - 페이징, 검색 기능 구현시 동일한 자원에 특정 조건을 덧붙이는 동작을 요구함
 - `URL`의 구성 중 Query Component를 활용할 수 있음
 - `?` 뒤에 오는 것이 `Query Component`, 서버에 동적으로 자원을 요구하거나 표현 형식을 변환한다
  > [Pagination 만들기](Page/Pagination.md)
 - `Query Component`는 `인자 이름 = 값` 조합으로 인자를 전달하며 `&`로 각 인자를 부분함
 - `Spring`에서 `Query Component`를 메서드로 가져오기 위해서는 `RequestParam` 활용 가능
 ```Java
 @GetMapping("/query-test")
    public void queryParams(
            @RequestParam("name")
            String name,
            @RequestParam(value = "age", required = false)
            Integer age,
            @RequestParam(value = "height", defaultValue = "175")
            Integer height,
            @RequestParam("weight")
            Integer weight
    ) {
    }
 ```
 >✏ `RequestParam`에는 `required`와 같은 `defaultValue` 인자 전달 가능

