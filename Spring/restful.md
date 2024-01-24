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
    >✏ 실질적으로 구현하기에는 난이도가 높음, 모든 원칙을 100% 지키기는 어려우며 `RESTful`한 API를 목표로 둔다

