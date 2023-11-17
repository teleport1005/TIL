## Markup 기본 문법 정리

✏..💻

### Headings - 문단 제목
- 제목, 부제 등을 표현할 때는 `#`을 사용
- `#`은 6개까지 사용할 수 있으며 많을 수록 더 작은 범위의 문단을 의미

### Emphasis - 글 강조
- `**`: 앞뒤로 사용시 해당 글귀 굵어짐 **굵어짐**
- `*`: 앞뒤로 사용시 해당 글귀 기울어짐 *기울어짐*
- `***`: 상기 두 가지를 모두 적용 가능 ***모두 적용***

### Block Quotes - 인용문
- 문단의 시작에 `>`를 작성

아래는 예시입니다.
> A quotation is the repetition of a sentence, phrase, or passage from speech or text that someone has said or written.

### Lists - 목록
- `1.` 등을 문장 시작에 붙이면 글의 순서 표현 가능
- `-`, `*`, `+` 등으로 사용시 순서 표현이 없는 리스트 작성 가능
- 목록 하위에 `Tap`을 사용 후 작성시 하위 목록으로 작성 가능  

아래는 예시입니다.
1. 기상
2. 커피 끓이기
3. 코딩 연습하기
    - Java

### Code - 코드
- 코드를 표현하고 싶을 때에는 `` ` ``(백틱)으로 감싸서 표현이 가능
- 작성하고 싶은 코드에 백틱이 포함되어 있다면 두 개의 백틱으로 감싸서 표현 가능
- 여러 줄의 코드를 표현하고 싶을 때에는 백틱 세 개를 사용하는 확장 문법 사용 가능  

아래는 예시입니다.
```
public class Main {
  public status void main(String[] args) {
    System.out.println("Hello Java!");
  }
}
```
- 해석 서비스에 따라 코드에 사용하는 언어를 알려주면 해당 언어의 문법에 맞게 색 변화 적용 가능  

아래는 예시입니다
```java
public class Main {
  public status void main(String[] args) {
    System.out.println("Hello Java!");
  }
}
```

### Horizontal Rules - 가로줄
- 가로 구분선 사용시 `---` 사용  

아래는 예시입니다
---

### Links - 링크
- `<>` 안에 링크 작성시 연결 가능  
- `[]()` 대괄호 안에 텍스트, 소괄호 안에 링크 작성시 텍스트 클릭으로 링크 접속 가능

### Images - 이미지
- `![]()` 대괄호에 이미지 이름, 소괄호에 이미지 위치 삽입시 이미지 추가 가능  
**웹 상의 이미지도 추가 가능**

