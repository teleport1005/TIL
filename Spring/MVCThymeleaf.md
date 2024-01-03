## MVC 패턴
- 사용자 인터페이스를 비즈니스 로직으로부터 분리하는 것을 목표로 만들어진 디자인 패턴
### Model
- 어플리케이션을 표현하기 위한 데이터 그 자체 및 데이터를 관리(비즈니스 로직)하는 구조
- 데이터의 변화를 View에 통보
### View
- 어떠한 형태로든 사용자에게 정보가 표현되는 부분
- 데이터를 받으면 그 데이터의 표현을 결정
- View의 표현은 Model의 (데이터의) 상태에 따라 변화
### Controller
- 사용자의 입력을 View를 통해 받고, Model이 이해할 수 있는 형태의 명령으로 변환하여 Model에게 전달

## Thymeleaf
- Thymeleaf는 준비된 HTML의 문서에 빈칸을 채워넣는 용도로 활용
```html
<h1 th:text="${message}"></h1>
```
>Thymeleaf는 이 h1 요소에 넘겨받은 model에 있는 데이터 중 이름이 message 인 데이터를 찾아서, h1에 전송시켜 줌

  ### 조건부 
  ```html
  <h1>Welcome</h1>
  <div th:if="${isLoggedIn}">
    <p>You are logged in.</p>
  </div>
  <div th:unless="${isLoggedIn}">
    <p>Please log in.</p>
  ```
  >model 에 추가한 isLoggedIn 의 값에 따라 결과가 다르게 출력됨

  ### 반복
  ```html
   <h1>Item List</h1>
  <div>
    <p th:each="item: ${itemList}">[[${item}]]</p>
  </div>
  ```
  >itemList 가 가지고 있는 아이템의 갯수만큼 p 요소를 반복하게 되고, p 요소 내부에서 item 의 이름으로 ${item} 과 같이 활용

