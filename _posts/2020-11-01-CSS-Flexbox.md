---
title: CSS Flexbox 정리
layout: post
categories: [CSS]
description: ""
customexcerpt: "CSS: flexbox "
comments: true
---

* hello
{:toc}


## Flexbox : 박스와 아이템들을 행/열 자유자재로 배치시켜줄 수 있는 유연한 layout
 우리는 css로 html의 속성 값들을 디자인할 때, 크게 두 가지의 속성을 변경하게 된다.
 1. 컨테이너 박스
 2. 박스 내의 각각의 아이템
 
![박스와 아이템](/assets/img/flex1_.jpg)
 
 
 **main axis 파악하기** 
 - flexbox를 제대로 사용하기 위해선 중심축(main axis)과 반대축(cross axis)를 먼저 알아야 한다.
 
 ![main axis / cross axis](/assets/img/flex2_.jpg)
  

## 컨테이너 박스의 Flexbox 속성
 - 컨테이너, 즉 parent의 flexbox 속성값에 대해 알아보자.
 - 여기 4개의 박스가 있다. div 태그로 만들어진 박스들은 block level로, 한 줄에 한 상자만 들어갈 수 있다.
 - div 박스들은 컨테이너의 너비 한 줄을 다 차지하게 되지만, 여기선 item 클래스의 아이템들의 속성을 너비 40px, 높이 40px로 수정했다고 가정한다.
 
 ![컨테이너1](/assets/img/flex3_.jpg)
 
 - column으로 배열되어 있으므로, 이 컨테이너의 main axis: column 으로 분석할 수 있다.
 - 그렇지만 컨테이너를 행으로 배열하고 싶다면 어떻게 해야할까? 이 때 flexbox를 이용하는 것이다.
 - flexbox를 적용하기 위해서는 컨테이너의 display를 flex로 지정해줘야 한다.
 
 ![display: flex;](/assets/img/flex4_.jpg)
 - flexbox가 적용되자 축이 row로 바뀐 것을 볼 수 있다.
 


## flex-direction ##
 - 박스의 방향을 변경해보자. reverse는 순서도 바뀐다.
 - flex-direction: row;
 - flex-direction: row(기본값) || row-reverse || column || column-reverse;
 
 ![flex-direction](/assets/img/flex5_.jpg)
 
## flex-wrap ##
 - 기본적으로 아이템들의 갯수에 상관 없이 모두 한 줄에 들어가게 되지만, 속성을 바꿔서 한 줄이 차면 다음줄로 줄바꿈 되도록 할 수 있다.
 - flex-wrap: nowrap;
 - 속성값: nowrap(기본값) | wrap | wrap-reverse;
 
 ![flex-wrap](/assets/img/flex6_.jpg)
 
 
## flex-flow ##
 - flex-direction, flex-wrap이 순서대로 결합된 단축 속성이다. 각 속성은 띄어쓰기로 구분한다.
 - 기본값은 row nowrap 
 - 예제) flex-flow: column wrap;
 
 
## justify-content ##
 - 중심축(main axis)을 기준으로 아이템들을 어떻게 배치할 것인지 결정할 때는 justify-content의 속성값들을 이용한다.
 - justify-content: flex-start;
 - 속성값: flex-start(기본값: 왼->오 / 위->아래) | flex-end(순서 유지) | center | space-between | space-around | space-evenly;
 
 ![justify-content](/assets/img/flex7_.jpg)
 
 - space-around: item들이 각자 양 옆에 자신만의 space를 동일하게 가지고, 서로의 space를 더한 만큼 떨어진다. 끝의 item은 자신의 space만큼만 떨어지도록 배치된다.
 - space-between: 첫번째 item은 start-line부터 시작하고, 마지막 item이 end-line에 맞춰지도록 균등 분배된다.
 - space-evenly: 모든 공간이 균일하도록 배치된다.
 
 
## align-items ##
 - 반대축(cross axis)을 기준으로 아이템들을 어떻게 배치할 것인지 결정할 때는 align-items의 속성값들을 이용한다.
 - 기본값은 stretch로, 아이템의 content 크기와는 상관 없이 컨테이너의 너비 혹은 높이를 다 채운다.(이 경우 cross axis가 column이므로 높이를 다 채운다.)
 - align-items: stretch;
 - 속성값: stretch(기본값) | flex-start | flex-end | center | baseline;
 
 ![align-items](/assets/img/flex8_.jpg) 
 - baseline: item들을 text 기준선에 맞춰 정렬한다.
 

## align-content ##
- item들이 container 내에서 multi-line일 경우, line 간의 cross axis 기준에서의 간격을 결정할 때는 align-content의 속성을 이용한다. (교차축 정렬)
- justify-content의 속성값들을 그대로 사용할 수 있고, single line일 경우 의미가 없다.
- align-content: normal;
- 속성값: normal(기본값) | flex-start | flex-end | center | space-around | space-between;

![align-content](/assets/img/flex9_.jpg)


## 아이템의 Flexbox 속성 
- 이제부터 아이템(child)의 속성값에 대해 다뤄본다.

## order ##
- 아이템 각각의 순서(order)를 정해줄 수 있다. 
- 모든 아이템의 기본값은 0이며, 숫자가 클수록 순서가 뒤로 밀린다. 
- 음수값도 사용 가능하기 때문에, order를 지정하지 않은 아이템(순서 기본값 0)보다 앞으로 배치할 수 있다.
- order: 0;

![order](/assets/img/flex10_.jpg)


## flex-grow ##
- 컨테이너가 커질 때 아이템이 컨테이너 공간을 차지할 비율을 결정한다.
- 기본값은 0으로, flex-grow를 설정하지 않을 시 아이템들은 컨테이너의 크기에 상관없이 자신의 고유 크기를 유지한다.
- 음수값은 허용되지 않는다.
- 아이템2의 flex-grow: 2;

![flex-grow](/assets/img/flex11_.gif)


## flex-shrink ##
- flex-shrink는 item의 width나 height에 영향을 받는다.
- 컨테이너가 작아진 만큼 지정한 flex-shrink 비율에 따라 아이템의 크기가 줄어든다.
- 계산이 까다로워 혼동이 있을 수 있으므로 가능한 사용하지 않는 것이 좋다.


## flex-basis ##
- 아이템들이 컨테이너 공간을 얼마나 차지해야 하는지 명시한다.(아이템의 기본 너비 설정)
- 기본값은 auto로, content를 제외한 여분의 공간이 flex-grow나 flex-shrink에 지정된 값에 맞춰 변형된다.
- 속성은 auto나 content와 같은 키워드이거나 px, em, % 등의 단위 값으로 지정할 수도 있다.
- flex-basis가 0일 경우 content 주위의 여분의 공간은 고려되지 않는다.

![flex-basis](/assets/img/flex12_.jpg)


## flex ##
- flex-grow, flex-shrink, flex-basis 순서대로 결합된 단축 속성이다. 각 속성은 띄어쓰기로 분할한다.
- flex-grow를 제외한 shrink와 basis는 생략할 수 있다.
- flex: 1; === flex-grow: 1;
- 기본값 flex: 1 1 0;
- 여기서 본래 flex-basis의 기본값은 auto지만, flex 단축에서 생략할 경우 0이 적용된다는 점을 주의해야 한다.


## align-self ##
- 각 아이템 별로 정렬할 때 사용된다.
- align-items는 모든 아이템의 정렬을 cross axis 기준으로 변경하지만 일부 아이템을 align-self로 따로 정렬할 수 있다.
- align-self는 align-items 사용 후에 오버라이딩(overriding)해서 사용할 수 있다. 즉, align-items 속성보다 우선시된다.
- 속성값: auto | flex-start | flex-end | center | baseline | stretch;

![align-self](/assets/img/flex13_.jpg)


## 참고 ##
- [CSS-TRICKS](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [FlexBoxFroggy 게임 하러가기](https://flexboxfroggy.com/#ko)

