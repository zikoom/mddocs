## flex Item 속성 알아보기

flex item을 직접 목표로 하여 더 상세한 설정을 할 수 있습니다. 우리는 이것을 다음 세가지 속성을 통해 가능합니다.


* flex-grow
* flex-shrink
* flex-basis

세가지 속성에 대해 이야기 하기 전에, __available space__ 에 대해 먼저 이야기해 보겠습니다. 왜냐하면 위의 세가지 속성을 바꾸는 것은, __available space__ 을 flex itme에게 분배하는 방법의 변경을 의미하기 때문입니다.

<br />
<img src=https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox/basics7.png />
<br />

500px width를 가지는 컨테이너 안에 100px width 아이템이 세 개 있습니다. 이 때 세 개의 아이템을 보여주는 데 필요헌 width (너비) 는 300px입니다. 이 때 남는 200px이 available space 입니다. flex-box의 초기값을 변경하지 않았다면, 마지막 아이템 이후의 공간이 available space가 됩니다.

### flex-basis

```flex-basis``` 는 availbale space를 available space로써 남겨 둘 때 item의 크기를 정의합니다. initial valu는 ```auto``` 입니다. 만약 flex-item이 width를 가지고 있다면 해당 width 값이 flex-basis가 됩니다. flex-item이 width를 가지고 있지 않다면 content-width가 flex-basis값으로 사용됩니다.

### flex-grow

```flex-grow``` 값이 양의 정수로 설정 되어 있다면 flex item은 주축을 따라 크기가 늘어날 수 있습니다. 만약에 늘어날 수 있는 또다른 flex item 이 있다면 해당 공간을 비율로 차지합니다. 각각의 flex item은 본인에게 설정된 flex-grow / (자신을 포함한 모든 형제 flex-item flex-grow의 합)
의 비율로 available space를 추가로 차지합니다.


### flex-shrink

```flex-shrink``` 는 부족한 공간을 어떻게 처리할지를 다룹니다. flex-container가 내부 item들을 보여주기에 충분한 공간을 가지고 있지 않고 ```flex-shrink``` 값이 양의 정수라면 flex-item은 flex-basis보다 작게 줄어듭니다.


이미지 출처 및 원문 내용: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox