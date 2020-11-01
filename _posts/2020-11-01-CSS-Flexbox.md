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
 
![박스와 아이템](/assets/img/flex__1.jpg)
 
 
 **main axis 파악하기** 
 - flexbox를 제대로 사용하기 위해선 중심축(main axis)과 반대축(cross axis)를 먼저 알아야 한다.
 
 ![main axis / cross axis](/assets/img/flex_2.jpg)
  

## 컨테이너 박스의 Flexbox 속성
 - 여기 6개의 박스가 있다. div 태그로 만들어진 박스들은 block level로, 한 줄에 한 상자만 들어갈 수 있다.
 ![컨테이너1](/assets/img/flex_3.png)
 - column으로 배열되어 있으므로, 이 컨테이너의 main axis: column 으로 분석할 수 있다.
 - 그렇지만 컨테이너를 행으로 배열하고 싶다면 어떻게 해야할까? 이 때 flexbox를 이용하는 것이다.
 - flexbox를 적용하기 위해서는 display를 flex로 지정해줘야 한다.
 
 ![display: flex;](/assets/img/flex_4.png)
 - flexbox가 적용되자 축이 바뀐 것을 볼 수 있다.


## flex-direction ##
 - 박스의 방향을 변경해보자. 
 - 속성값: row(기본값); row-reverse(순서바뀜); column; column-reverse;
 
 ![flex-direction](/assets/img/flex_5.png)
 
## flex-wrap ##
 - 기본적으로 아이템들의 갯수에 상관 없이 모두 한 줄에 들어가게 되지만, 속성을 바꿔서 한 줄이 차면 다음줄로 줄바꿈 되도록 할 수 있다.
 - 속성값: nowrap(기본값); wrap; wrap-reverse;
 
 ![flex-wrap](/assets/img/flex_6.png)

## justify-content ##
 - 중심축(main axis)을 기준으로 아이템들을 어떻게 배치할 것인지 결정할 때는 justify-content의 속성값들을 이용한다.
 - 속성값: flex-start(기본값: 왼->오 / 위->아래); flex-end(순서 유지); center; space-around; space-evenly; space-between;
 
 ![justify-content](/assets/img/flex_7.png)
 
## align-items ##
 - 반대축(cross axis)을 기준으로 아이템들을 어떻게 배치할 것인지 결정할 때는 align-items의 속성값들을 이용한다.
 추후 업데이트 . . .
