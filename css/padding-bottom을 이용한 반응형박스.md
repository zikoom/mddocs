padding-bottom을 이용한 반응형박스
===

padding-bottom, padding-top 속성의 퍼센트 값은 containing block 가로 길이를 기준으로 결정됩니다.
이것을 이용하여 가로, 세로 비율이 유지되는 박스를 만들 수 있습니다.

https://developer.mozilla.org/en-US/docs/Web/CSS/padding-bottom 에서 Values -> percentage 참조


## containing block 출처: (https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block)

position property의 값에 의해 결정되는 영역입니다. 어떤 요소의 position이
- static, relative sticy

중 하나라면, containing block은 가장 가까운 조상 block container의 content box 영역이 됩니다.

position이 **absolute** 라면 containing block은 static이 아닌 position 값을 지니는 가장 가까운 조상 요소의 padding box가 됩니다.

<br/>

## padding-bottom을 이용하여 반응형 박스 만들기

상하 방향의 padding 영역을 늘림으로써 우리가 원하는 비율의 박스를 만드는 것이 가능합니다.


```html
<div class="container">
  <div class="item"></div>
</div>
```


```css
.container {
  width: 200px;
}

.item {
  padding-bottom: 50%
}
```

<br />

container 길이의 절반의 높이를 가지는 박스를 만들 수 있습니다.