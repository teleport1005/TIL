## CSS Position
- 요소의 배치를 결정하는 속성
- static (기본값, 일반적인 요소 배치)
- relative
- absolute
- fixed
- sticky
- position 속성으로 방식, top, left, right, bottom으로 방향과 거리 결정

### relative
- 원래의 위치에서 주어진 위치만큼 멀어지게 이동
```javascript
.relative {
  position: relative;
  right: 0px;
  bottom: 30px;
}
```
- 다른 요소에는 영향을 미치지 않음
---
### absolute
- body 혹은 가까운 조상 요소를 기준으로 배치
```Javascript
.absolute {
  position: absolute;
  top: 200px;
  left: 450px;
}
```
- 다른 요소는 absolute가 없는 것처럼 재배치됨
---
### fixed
- 브라우저 화면을 기준으로 배치
```Javascript
.fixed {
  position: fixed;
  right: 20px;
  bottom: 20px;
}
```
- 스크롤을 해도 같은 위치에 고정된다
---
### sticky
- 설정한 시점부터 fixed가 됨
```Javascript
.sticky {
  position: sticky;
  top: 25px;
}
```

### z-index
- 순서를 배정
```Javascript
.box {
  z-index: 5;
}
```
- 높은 수가 가장 위쪽으로 배치됨