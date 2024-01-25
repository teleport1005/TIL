 ### JPA를 활용한 Query문 작성하기
   - JPA를 사용하게 되면서 단순한 데이터 작업 구문을 활용하였었다
   - 아래는 기본적인 사용 예시이다
   ```
   - findById - PK를 기준으로 READ
   - findAll - 전체 READ
   - save - CREATE
   - deleteById - PK를 기준으로 DELETE
   - delete - Entity를 기준으로 DELETE
   ```
   - 그 외 다양한 유형의 Query문을 JPA로 활용하여 사용하는 방법을 알아보자

   #### 데이터 출력(정렬) 활용

   ```Java
     // SELECT * FROM articles ORDER BY id DESC; // id를 기준으로 데이터 역순 정렬
     List<Article> findAllByOrderByIdDesc();
   ```

   ```Java
     // SELECT * FROM article ORDER BY writer DESC; // writer의 알파벳 역순으로 데이터 정렬
     List<Article> findAllByOrderByWriterDesc();
   ```

   ```Java
     // SELECT * FROM article ORDER BY title; // title의 알파벳 순으로 데이터 정렬
     List<Article> findAllByOrderByTitle();
   ```

  #### 특정 데이터 조회 활용 

   ```Java
   // 특정 article의 이전 글 목록 조회
   // SELECT * FROM article WHERE (id) > ?; // 해당 글의 id보다 큰 id의 article 조회
     List<Article> findAllByGreaterThan(Long id); // article의 id보다 큰 article List 조회
   ```

   ```Java
   // 특정 article의 다음 글 목록 조회
   // SELECT * FROM aritlce WHERE (id) < ?; // 해당 글의 id보다 작은 id의 article 조회
    List<Article> findAllByLessThan(Long id); // article의 id보다 작은 article List 조회
   ```

   ```Java
   // 특정 article의 다음 글 목록 순차 조회
   // SELECT * FROM article WHERE id < ? ORDER BY id DESC;
   List<Article> findAllByIdLessThanOrderByIdDesc(Long id);
   ```
   > ✏ `ORDER BY id DESC`는 `id` 필드를 내림차순으로 정렬하라는 의미이다.  
   > ✏ 이렇게 되면 가장 큰 `id`부터 가장 작은 `id`로 정렬된다. -> 최신순 정렬  
   > ✏ 다음 글을 가지고 올 때, 가장 큰 `id`보다 작은 `id`를 가진 글 중에서 제일 큰 `id`를 가져옴으로써, 
        다음글을 가져오는 것이다

   ```Java
   // 특정 aritlce의 다음 글 조회
   // SELECT * FROM article WHERE id > ? LIMIT 1;
   Optional<Article> findFirstByIdAfter(Long id);
   ```      

   ```Java
   // 특정 article의 이전 글 조회
   // SELECT * FROM article WHERE id > ? ORDER BY id DESC LIMIT 1;
   Optional<Article> findFirstByIdLessThanOrderByIdDesc(Long id);
   ```

  ```Java
  // 제목에 특정 문구가 포함괸 글의 목록을 조회
  // SELECT * FROM article WHERE title LIKE %특정 문구%;
  List<Article> findAllByTitleContaining(String title);
  ```      

