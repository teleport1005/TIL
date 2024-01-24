## Serializaition (직렬화)
- 메모리상에 저장된 데이터를 전송 가능한 형태로 바꾸는 작업  
-> Java Heap 메모리 내에 저장된 데이터를 인간이 읽을 수 있는 글자의 형태로 바꾸는 것
```Java
public class ArticleDto {
  private String title;
  private String content;
}
// Java 메모리가 가지고 있는 데이터
```
```YAML
title: "게시글 제목"
content: "게시글 내용"
읽을 수 있게 표현된 문자열 데이터
```

 ### JSON
 - `JSON`: Lightweight data-interchange format
 - 데이터를 주고받는 것에 활용할 수 있는 `데이터 표현 방식`
 ```JSON
 {
  "title": "게시글 제목",
  "content": "게시글 내용"
 }
 ```

> ✏ 직렬화는 Java의 고유 기술인 만큼 최적화나 레퍼런스 타입에 제약이 없는 장점이 있다  
> ✏ JSON은 가독성이 뛰어나고 파이썬이나 자바 스트립트에서도 사용 가능하다는 장점이 있다  
> ✏ 직렬화와 JSON은 목적에 따라 적절히 사용하나 보다 범용적인 JSON을 이용하는 추세가 늘고 있다


 