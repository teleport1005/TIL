## CSS Box Model
- 요소를 상자를 바탕으로 구성한다
1. content: 요소 가장 내부
2. padding: 테두리부터 요소 내용까지의 공간
3. border: 요소의 테두리
4. margin: 테두리부터 외부 요소와의 공간
---
### Block & Inline
- Block 요소
>h1, p 등 줄바꿈 동작을 만드는 요소
- Inline 요소
>a 등 줄바꿈 영향을 미치지 않는 요소
---
### width & height
- 가로 세로 크기를 설정
```JavaScript
#box-bodel {
  width: 200px;
  height: 200px;
}
```
---
### margin
- 요소와 요소 간격 조정
```JavaScript
.margin { 
  /* 내용과 외부 사이의 공간을 벌림 */
  margin-top: 50px;
  margin-right: 100px;
  margin-bottom: 150px;
  margin-left: 200px;
}
```
---
### padding
- 테두리와 요소의 간격 조정
```JavaScript
.padding { 
  /* 내용과 테두리 사이의 padding 공간을 벌림*/
  padding-top: 20px;
  padding-right: 30px;
  padding-bottom: 40px;
  padding-left: 50px;
}
```
- 4 방향이 모두 동일할 때에는 축약하여 사용이 가능
```JavaScript
/* 4 방향 모두 거리를 벌림 */
.margin-all { 
  margin: 40px;
}
.padding-all {
  padding: 40px;
}
```
---
### border
- 요소의 테두리
- border-width: 테두리 굵기
- border-style: 테두리 선 형식
- border-color: 테두리 색
- 축약이 가능하다
```JavaScript
.border-short {
  border: 2px solid black;
   /*굵기 형식 색상*/
}
```

