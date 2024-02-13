## Redis 활용

### HttpSession
- Spring Boot에서 session을 생성할 경우 Tomcat 서버에서 `JSESSIONID` 쿠키를 발급
- 위 값을 이용하여 클라이언트를 구별한다

### Session Clustering(HttpSession과 Redis)
- Session은 Spring Boot Application 단위로 관리된다
- 여러 서버 인스턴스를 만들고, session을 늘리게 된다면 데이터의 저장 여부가 갈릴 수 있다
  > 포트 번호를 바꾸면서 저장, 회수를 하면 정상적인 작동이 불가하다 
- 세션의 정보가 서버 단위로 공유가 되지 않을 때, `Redis`를 활용하여 공유 설정을 할 수 있다
  #### 1. 의존성 추가
  ```yaml
  implementation 'org.springframework.boot:spring-boot-starter-data-redis'
  implementation 'org.springframework.session:spring-session-data-redis'
  ```
  #### 2. 클래스 설정 추가(`EnableRedisHttpSession`)
  ```Java
  @EnableRedisHttpSession
  @SpringBootApplication
  public class SimpleSessionApplication {
    // ...
  }
  ```
  > 이후 Spring Boot가 Redis를 이용하여 세션 정보를 기록한다

  
### Redis Caching

```
CPU Cache
- RAM보다 읽기 쓰기 속도가 빠른 CPU 내에서 조회되는 임시 저장 장치
- 영속성을 위한 데이터는 파일 시스템, 빠른 활용을 위한 데이터는 메모리(RAM)에 저장
- 많이 사용되는 휘발성 데이터가 Cache에 저장된다
```

### Caching
- 임시 저장소에 데이터를 저장하는 것
>✏ RESTful 제약사항 중에도 Cacheability가 있다
- Redis의 In Memory 데이터베이스에 저장함으로서 빈번하게 접근하게 되는 데이터를 빠르게 조회
- 시간과 자원을 감소시키는 기술을 `Caching`이라고 칭한다

### Cache 기본 정보
- `Cache Hit`(캐시 적중): 캐시 접근시 찾는 데이터가 있는 경우
- `Cache Miss`(캐시 미스): 캐시 접근시 찾는 데이터가 없는 경우
- `Evivtion Policy`(삭제 정책): 캐시 공간 부족시 공간 확보 정책
- `Caching Strategy`(=Lazy Loading): 데이터 저장과 캐시 확인 전략
  > 데이터를 조회할 때 항상 캐시를 체크하는 방식으로, 데이터가 있으면 캐시에서, 없으면 원본에서 가져와 저장 
  > 조회시 시간이 더 소요되고 캐시 데이터가 최신이라는 보장이 없지만 필요한 데이터만 저장이 가능
- Write Through: 데이터 작성시 항상 캐시에 작성 후 이후 원본으로 갱신하는 방식
  > 캐시가 항상 동기화되어 있으며 캐시 데이터는 최신으로 유지 
  > 자주 사용하지 않는 데이터도 캐시되며, 작성이 항상 캐시를 거치기 때문에 시간이 소요
- Write Behind(Write Back): 캐시에 데이터 작성 후 일정 주기로 원본에 반영하는 방식
  > 작성이 잦지 않은 경우 데이터베이스 부하를 줄일 수 있음  
  > 캐시 데이터가 원본에 저장되기 전 문제가 발생할 경우 데이터 소실 가능성 있음



