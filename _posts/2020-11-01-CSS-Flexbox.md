---
title: CSS Flexbox 정리
layout: post
categories: [CSS]
description: ""
customexcerpt: "CSS: flexbox "
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
 - 속성값: row(기본값); row-reverse; column; column-reverse;
 
 ![flex-direction](/assets/img/flex5_.jpg)
 
## flex-wrap ##
 - 기본적으로 아이템들의 갯수에 상관 없이 모두 한 줄에 들어가게 되지만, 속성을 바꿔서 한 줄이 차면 다음줄로 줄바꿈 되도록 할 수 있다.
 - flex-wrap: nowrap;
 - 속성값: nowrap(기본값); wrap; wrap-reverse;
 
 ![flex-wrap](/assets/img/flex6_.jpg)

## justify-content ##
 - 중심축(main axis)을 기준으로 아이템들을 어떻게 배치할 것인지 결정할 때는 justify-content의 속성값들을 이용한다.
 - 속성값: flex-start(기본값: 왼->오 / 위->아래); flex-end(순서 유지); center; space-around; space-evenly; space-between;
 
 ![justify-content](/assets/img/flex7_.jpg)
 
 - space-around: item들이 각자 양 옆에 자신만의 space를 동일하게 가지고, 서로의 space를 더한 만큼 떨어진다. 끝의 item은 자신의 space만큼만 떨어지도록 배치된다.
 - space-between: 첫번째 item은 start-line부터 시작하고, 마지막 item이 end-line에 맞춰지도록 균등 분배된다.
 - space-evenly: 모든 공간이 균일하도록 배치된다.
 
 
## align-items ##
 - 반대축(cross axis)을 기준으로 아이템들을 어떻게 배치할 것인지 결정할 때는 align-items의 속성값들을 이용한다.
 - 기본값은 stretch로, 컨테이너의 너비 혹은 높이를 다 채운다.(이 경우 row로 정렬되어 있으므로 높이를 다 채운다.)
 - 속성값: stretch(기본값); flex-start; flex-end; center; baseline
 
 ![align-items](/assets/img/flex8_.jpg) 
 - baseline: item들을 text 기준선에 맞춰 정렬한다.
 

## align-content ##
- item들이 container 내에서 multi-line일 경우, line 간의 cross axis 기준에서의 간격을 결정할 때는 align-content의 속성을 이용한다. (교차축 정렬)
- justify-content의 속성값들을 사용할 수 있다.
- 추후 업데이트 . . . 
