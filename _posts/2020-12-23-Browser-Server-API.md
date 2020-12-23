---
title: Browser, Server, APIs, HTTP, Ajax, Fetch
layout: post
categories: [Server]
description: ""
customexcerpt: "Server: Browser, Server, APIs, HTTP, Ajax, Fetch"
comments: true
---

* hello
{:toc}

## Browser ##
 - 웹에서 페이지를 찾아 보여주고, 사용자가 하이퍼링크를 통해 다른 페이지로 이동할 수 있도록 하는 프로그램
 - 브라우저의 종류: Internet Explorer(IE), FireFox, Safari, Chrome, Opera
 - 오픈소스 브라우저(파이어폭스, 사파리, 크롬)의 점유율이 높음
 
 <br>
 
 **브라우저의 기능**
  - 사용자가 선택한 자원을 서버에 요청하고 표시해줌
  - 자원은 보통 HTML 문서이며, 자원의 주소는 URI에 의해 정해진다. 브라우저가 이 HTML 파일을 해석해서 표시
  - 브라우저의 사용자 인터페이스는 표준이 정해져 있지는 않지만 일반적인 요소들이 있다.
      - URI를 입력할 수 있는 주소 표시 줄
      - 이전 버튼, 다음 버튼
      - 북마크
      - 새로 고침 버튼, 현재 문서의 로드를 중단할 수 있는 정지 버튼
      - 홈 버튼
  
 <br>
 
 **브라우저의 기본 구조**
  - 사용자 인터페이스: 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분
  - 브라우저 엔진: 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어
  - 렌더링 엔진: 요청한 콘텐츠를 브라우저 화면에 표시.
  - 통신: HTTP 요청과 같은 네트워크 호출에 사용됨. 플랫폼 독립적인 인터페이스이며, 하부에서 실행됨.
  - UI 백엔드: 콤보 박스와 창 같은 기본적인 장치를 그림. 플랫폼에서 명시하지 않은 일반적인 인터페이스로, OS 사용자 인터페이스 체계를 사용.
  - 자바스크립트 해석기: 자바스크립트 코드를 해석하고 실행(크롬의 경우 V8 엔진)
  - 자료 저장소: 자료를 저장하는 계층.
  
 <br>
 
## Web server ##
 - 자원을 제공하는 주체
 - 손님(클라이언트)이 커피를 주문하면 카페(서버)가 창고(데이터베이스)에 있는 원두를 꺼내 커피를 제조해 손님에게 제공
 - Web Arcitecture: 클라이언트의 user message -> server가 받음 -> DB에서 message 꺼냄 -> server가 message를 클라이언트에게 응답
 - 하드웨어 측면에서, 웹 서버의 소프트웨어와 웹 사이트의 컴포넌트 파일(HTML, CSS, JS)을 저장하는 컴퓨터로서, 인터넷에 연결되어 있으며 웹에 연결된 다른 기기들이 웹 서버의 데이터를 주고받을 수 있도록 한다.
 - 소프트웨어 측면에서, 기본적으로 사용자가 호스트 파일에 접근하는 것을 관리한다. HTTP 서버는 URL과 HTTP(브라우저가 웹 페이지를 사용자에게 보여주기 위해 사용하는 프로토콜)의 소프트웨어 일부
 - 브라우저는 HTTP를 통해 파일을 요청하고, 요청이 웹 서버(하드웨어)에 도달하면 웹 서버(소프트웨어)가 요청된 문서를 HTTP를 이용해 보내준다.

![browser](/assets/img/server.png)

<br>

## APIs ##
- Application Programming Interfaces: 프로그래밍 되어있는 애플리케이션과 의사소통 가능한 매개체
- 클라이언트가 서버의 데이터베이스에 어떤 리소스가 들어있는지 모른다면?
- 클라이언트가 데이터베이스의 리소스를 잘 활용할 수 있도록 서버가 제공하는 인터페이스
    - 서버 자원을 잘 가져다 쓸 수 있도록 만들어 놓은 인터페이스(매개체)
    - 카페(서버)가 메뉴판(API)을 제공해줘야 손님(클라이언트)이 이용 가능
- 복잡한 기능을 더 쉽게 만들 수 있도록 프로그래밍 언어로 제공된 인터페이스로, 소프트웨어 프로그램(애플리케이션) 내부에 존재하는 기능 및 규칙의 집합
- GET/messages(메시지 전달) -> server: POST/messages(메세지 저장)

<br>

 **APIs in client-side JS**
  - 자바스크립트 언어 자체에 포함된 것이 아니라, 핵심 자바스크립트 언어 위에 구축되어 추가적인 기능을 제공하는 것
  - API는 두가지로 분류된다.
      - Browser APIs: 웹 브라우저에 내장되어 자바스크립트 위에서 추가 기능을 보다 쉽게 구현할 수 있게 한다.
          - Web Audio API는 브라우저의 오디오를 조작하기 위한 자바스크립트 구조를 제공한다.
      - Third-party APIs: 브라우저에 내장되어 있지 않고 일반적으로 타사 플랫폼에 내장되어 웹 페이지에서 이러한 플랫폼의 기능 중 일부를 사용할 수 있다.
          - Twitter API, Facebook API
  
 **JavaScript와 APIs**
  - JavaScript libraries: 사용자 지정 기능이 포함된 하나 이상의 JavaScript 파일
      - jQuery, Mootools, React
  
  - JavaScript frameworks: HTML, CSS, JS 등 파일들의 패키지
  - 라이브러리의 경우 메소드 호출 시 개발자에게 제어권이 있지만, 프레임워크에서는 프레임워크가 개발자의 코드를 호출한다.
 
 <br>
 
## HTTP ##
 - Hypertext Transfer Protocol: HTML과 같은 문서를 전송하기 위한 프로토콜(규약, 규칙)
 - 클라이언트와 서버가 통신하기 위한 규칙  
 - 요청과 응답으로 이루어진다.
    - client: 요청 -> server: 응답 -> client
 <br>
  
 **HTTP요청의 구성**
  - Header + Body
   - 헤더: 어디서 보내는 요청인지(origin)/ 컨텐츠 타입은 무엇인지/ 어떤 클라이언트를 이용해 보냈는지(user-agent)
   - 바디: 메소드에 따라 가지고 있을 수도, 없을 수도 있다. 서버에 데이터를 보내기 위한 공간
  
  - HTTP 응답도 헤더와 바디로 이루어져 있다.
 <br>
 
 **HTTP의 속성**
  - stateless: 각 요청은 모두 독립적이기 때문에 state가 없다.(context문맥이 형성되지 않는다.)
  - connectionless: 한 번의 요청에는 한 번의 응답을 한다. 응답 후 연결이 종료되기 때문에 더 이상 응답할 수 없다.
 
 <br>
 
 **HTTP의 메소드**
  - GET: 서버에 자원을 요청
  - POST: 서버에 자원을 생성
  - PUT: 서버의 자원을 수정
  - DELETE: 서버의 자원을 제거
  
 <br>  
 
## Ajax ##
 - JavaScript를 사용한 비동기 통신, 클라이언트와 서버간에 데이터를 주고받는 기술
 - 이전에는 form 태그를 이용해 로그인 정보를 서버에 제출 시 새로운 페이지로 응답했다.
    - 로그인: form.html -> 응답: result.html
    - 페이지 내에서 필요한 정보만 바뀌는 것이 아닌, 아예 새로운 페이지 전체를 내려받기 때문에 속도가 느리고 페이지 전환으로 인한 깜빡임 현상(랜더)이 있었음.
 
 <br>
 
 - 페이지의 일부만 업데이트하기 위해 서버 응답에 따라 동적으로 페이지의 구성 요소를 변경한다.
 - dynamic web page
    - 서버와 자유롭게 통신: XMLHttpRequest(XHR) //API
    - 페이지 깜빡임 없이 seamless하게 작동: JavaScript와 DOM 이용
 => AJAX(Asynchronous JavaScript and XML)
 
 <br>
 
 - 방식의 변화: XHR get 요청, response 파싱 -> jQuery를 활용한 XHR -> fetch API

 <br>
 
 **fetch**
  - 클라이언트가 서버 자원을 가져오기 위해 사용하는 메소드(API)
  - 유연하고 강력한 조작이 가능하다.
  
```js
// XMLHttpRequest
let oReq = new XMLHttpRequest();
oReq.addEventListener('load', someFunction);
oReq.open('GET', 'URL')
oReq.send();

// jQuery ajax
$.ajax({
  url: 'url',
  method: 'GET',
  dataType: 'json'
})
  .done(json => console.log(json))
  .fail(xhr, status, errorThrown => {
  
  })
  .always(xhr, status => console.log('요청 완료'))
  
// fetch API
fetch('URL')
.then(response => response.json())
.then(json => {
  // DOM을 이용한 페이지 수정
})
.catch(err => console.log(err))
```

  
