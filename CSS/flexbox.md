## CSS Flexbox
- UI의 배치를 `Layout`이라 한다
- CSS의 Flexbox는 `Layout` 제작에 특화

### Flexbox
```html
<div class="container-flex">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
> 좌에서 우로 정렬 배치
```

### Flex Direction
주축의 방향을 결정할 수 있다
- row: 좌에서 우로 (기본값)
- column: 상에서 하로
- row-reverse: 우에서 좌로
- column-reverse: 하에서 상으로

3. flex-wrap
- wrap: 넘치는 요소를 다음줄에 출력한다.
- nowrap: 요소를 줄여서라도 한줄에 출력한다.


### 요소 정렬하기
`justify-content`  
주축의 방향에 맞춰 요소들을 정렬한다.
- flex-start: 주축의 시작 방향으로 정렬한다.
- flex-end: 주축의 끝 방향으로 정렬한다.
- center: 주축 가운데로 정렬한다.  

요소들 사이로 여백을 배치할 수도 있다.
- space-around: 각 요소 주변에 같은 여백을 배치한다.
- space-between: 요소 사이에만, 동일한 여백을 넣어준다.
양 끝 요소는 부모의 테두리에 닿는다.
- space-evenly: 모든 여백이 동일해진다.  

`align-items`  
교차축의 방향으로 요소를 정렬한다.
- flex-start: 교차축의 시작(row의 경우 위쪽) 방향으로 정렬
- flex-end: 교차축의 끝(row의 경우 아래쪽) 방향으로 정렬
- center: 교차축의 가운데로 정렬
