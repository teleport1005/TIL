## Pagination
- 조회 데이터의 개수가 많을 때 강제적으로 한정시켜 페이지로 나누는 기법
- 성능 향상 기대
- UX 향상

### Query Method 활용

```Java
// ID가 큰 순서대로 최상위 20개
List<Article> findTop20ByOrderByIdDesc();
// ID가 특정 값보다 작은 데이터 중 큰 순서대로 최상위 20개
List<Article> findTop20ByIdLessThanOrderByIdDesc(Long id);
```
>✏ [JPA를 활용한 Query문 작성](jpaQuery.md) 참조

- `findTop20ByOrderByIdDesc()` : ID의 역순(최신순)으로 상위 20개 조회
- `findTop20ByIdLessEqualOrderByIdDesc(Long id)` : 주어진 id 보다 ID가 작은 데이터를 ID 역순으로 상위 20개 조회

### PagingAndSortingRepository 기능 활용

```Java
// 20개 단위로 나누었을때, 0번째 페이지
Pageable pageable = PageRequest.of(0, 20);
```
- `JpaRepository`가 상속받고 있는 기능
- `Pageable` 기능을 이용하여 페이지에서 확인하고 싶은 데이터 개수 설정 

```Java
Page<Article> articleEntityPage = repository.findAll(pageable);
```
- Page에 모든 데이터 반환하여 사용

### URL 전달
- Pagination은 새로운 자원을 전달하는 것이 아닌 데이터 중 일부만 전달하는 것
- 따라서 동일한 URL에 `GET` Query Parameter 추가하여 활용
- 현재 조회하고 싶은 페이지와 한 페이지에서 필요한 데이터의 갯수가 필요
```URL
GET /articles?page=1&limit=20 // URL 주소
```
- `Controller`에서 구현
```Java
  @GetMapping
  public Page<ArticleDto> readAllPaged(
          @RequestParam(value = "page", defaultValue = "1")
          Integer page,
          @RequestParam(value = "limit", defaultValue = "20")
          Integer limit
  ) {
      return service.readAllPagination(page, limit);
  }
```
