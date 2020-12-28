---
title: node.js를 이용한 http 서버 구축/응답
layout: post
categories: [Server]
description: ""
customexcerpt: "Server: HTTP request/response"
comments: true
---

* hello
{:toc}

## node.js ##
 - JavaScript를 기계어로 compile 해주는 엔진(chrome: v8)으로 빌드되어 JavaScript가 구동되는 환경
 - 이벤트 기반의 non-blocking I/O model이다.
    - 이벤트: 유저의 버튼 클릭, 네트워크에 리소스 요청 등
    - non-blocking: 다음 함수의 실행이 현재 함수의 종료를 기다리지 않고 실행됨
    - I/O model: input을 주면 ouput을 반환하는 모델
    
 <br>
    
 **node core modules**
  - node.js는 3가지 타입의 module을 쓸 수 있다.
      - core modules, local modules, third party modules
  - node.js가 시작되면 자동으로 로드되기 때문에 별도의 설치 없이 사용 가능한 모듈이다.
  - 응용 프로그램에서 사용하기 위해서는 require() 메소드로 모듈을 가져와야 한다.
  - core module의 종류: http, url, querystring, path, fs, util
  
  ```js
  const module = require('module_name');
  ```
  
 <br>
 
 **npm**
  - node package manager: 응용 프로그램에 node.js 패키지를 설치하는 command line tool
  - 오픈 소스 node.js packages의 온라인 레파지토리
  - 유용한 모듈을 만들어 레포지토리에 게시할 수 있고 npm에 올라와있는 패키지는 터미널에서 npm을 통해 설치하여 사용할 수 있다.
  - node.js 설치 시 함께 포함되어 있으며, `npm -v` 명령어로 npm 버전을 확인할 수 있다.
  - 최신 버전 업데이트 시 `npm install npm -g`
  - 패키지 설치 시 `npm install 패키지이름`
  - package.json: 프로젝트 정보, 프로젝트 셋업에 대한 정보 등을 모아 관리하는 파일
  - package.json 파일의 dependency 항목에서 프로젝트에서 사용 중인 패키지 정보를 관리한다. 여러 명의 개발자가 하나의 프로젝트를 진행할 경우 패키지를 프로젝트에 포함시키는 대신 package.json을 통해 필요한 패키지를 설치할 수 있다.
      - 패키지를 package.json 파일의 dependency 항목에 추가하기 위해서는 설치 시 --save 옵션을 줘야 한다.
  - dev-dependency 항목에서는 프로젝트와 직접적인 관계는 없고 개발만을 위해 필요한 dependenciy를 관리한다.
      - 설치 시 --dev 옵션을 준다.
  - `npm init` : 'npm을 사용하는 프로젝트로 정의'한다는 뜻으로, 폴더에 package.json 파일이 생성된다.
  
    ```
    $ npm install --save nodemon
    $ npm install @babel/core --save-dev
    ```
    
    ```js
    // package.json
    {
      // project에 관한 정보
      "name": "",
      "version": "",
      "description": "",
      
      // 설정된 script 코드
      "scripts": {
        "start": "nodemon script.js",
        
      // 프로젝트에서 사용 중인 패키지 정보
      "dependencies": {
        "nodemon": "^2.0.6"
      }
      // 개발에 필요한 패키지 정보
      "devDependencies": {
        "@babel/core": ""
      }
    }
    ```
  
  <br>
  
## HTTP 서버 요청/응답 과정 ##
 - 웹에서 이루어지는 클라이언트와 서버 간의 데이터 교환 프로토콜
 - 요청(requests): 클라이언트(보통의 경우 브라우저)에 의해 전송되는 메시지
 - 응답(responses): 서버에서 응답으로 전송되는 메시지
 - 주소창에 url을 입력하는 get 요청 시 서버의 응답 과정을 알아보자.
 - http://www.google.com/int1/ko_kr/about/
   - http:// 사용하는 프로토콜을 정의
   - www.google.com 도메인 네임
   - /init1/ko_kr/about/ 서버 내에서 routing(분기)되는 주소
 1. 주소창을 통해 하는 요청은 모두 GET Request로, 서버에 url로 된 http request를 보내면,
 2. DNS(Domain Name Server)가 요청 받은 url의 ip로 응답해준다.
   - 요청과 응답 메세지 등 클라이언트와 서버 사이에 전송되는 모든 메세지는 TCP/IP 연결을 통해 전송된다. 
   - 서버가 요청을 승인하면 status code가 담긴 메세지를 클라이언트에 전송한다. "200 OK"는 요청 성공 메세지
   - 웹 서버의 routing(주소 탐색 규칙)에 따라 요청을 처리한다.
   - 서버가 웹사이트의 파일들을 데이터 패킷의 형태로 전송 프로토콜에 따라 브라우저에 전송한다.
   - 서버가 보내주는 자원(html, js file..)을 브라우저에서 처리한다. 즉 브라우저는 전송받은 데이터 패킷들을 조립하여 웹 사이트를 렌더링한다.
 
 <br>

 **TCP vs. UDP**
  - 전송 프로토콜
  - 응답으로 전송되는 데이터는 IP 주소를 통해 디바이스에 도착한 후 헤더에 있는 프로토콜 정보로 UDP 혹은 TCP 연결인지 확인한 후 각 헤더의 port number를 통해 목표 프로세스로 들어간다.
    - 기본적으로 80 포트를 사용한다.(주소 뒤 콜론과 함께 있는 숫자로, 없을 경우 80이 생략된 것)
    
  - 만약 웹 사이트가 데이터 전체로서 한 번에 전송된다면 한 번에 하나의 사용자만 다운로드 가능 할 것이다. 여러 웹 사용자가 동시에 웹 사이트를 이용 가능하게 하기 위해 데이터를 수천개의 작은 조각들로 전송한다.
  - 이 데이터 조각들을 패킷이라 하며 패킷을 전송하는 방식에 따라 TCP 혹은 UDP로 분류된다. 일반적으로 신뢰성이 높은 TCP 연결을 사용한다.
  - TCP(Transmission Control Protocol): IP와 함께 사용하는 프로토콜
    - 연결형 프로토콜로서 데이터의 흐름 제어가 가능하다. 패킷(데이터 조각)의 경로가 존재하며 속도가 느리고 신뢰성이 보장된다. 
    - 파일 전송과 같은 속도보다 신뢰성 있는 전송이 중요할 경우 사용
    
  - UDP(User Datagrm Protocol): 데이터를 데이터그램 단위로 처리하는 프로토콜
    - 비연결형 프로토콜로서 각 패킷은 독립적이며 서로 다른 경로로 전송된다. 속도가 빠르지만 신뢰성이 낮다.
    - 음악이나 동영상 스트리밍 같은 데이터가 일부 누락되어도 상관 없는 경우 사용
  
 <br>
  
 **cache**
  - 웹 캐시 또는 HTTP 캐시
  - HTTP responses를 일시적으로 저장하는 곳
  - 다음 HTTP request 조건이 만족될 때 까지 캐시에 저장한 리소스를 사용할 수 있다.

 <br>
 
 **HTTP status code**
  - "200 OK": 요청 성공
  - "201 Created": 요청이 성공하여 새로운 리소스가 생성됨(일반적으로 POsT, PUT 요청)
  - "304 Not Modified": 캐시 목적. 요청에 대한 응답이 수정되지 않음. 클라이언트는 응답의 캐시된 버전을 사용할 수 있음
  - 400 번대 code: 클라이언트 에러
    - "400 Bad Request": 잘못된 문법으로 인해 서버가 요청을 이해할 수 없음
    - "403 Forbidden": 클라이언트가 콘텐츠에 접근할 권한이 없음 => 거절
    - "404 Not Found": 요청받은 리소스를 찾을 수 없음
    
  - 500 번대 code: 서버 에러
    - "500 Internal Server Error": 서버가 처리할 수 없는 요청
 
 <br>
 
## HTTP 메시지의 구성 ##
 **HTTP Request**
 
 ![request](/assets/img/httpreq.png)
 
 <br>
 
 **HTTP Response**
 
 ![request](/assets/img/httpres.png)
 
<br>

## HTTP transaction ##
 **http 모듈 불러오기**
 
 ```js
 const http = require('http');
 ```
 
 <br>
 
 **서버 생성**
  - createServer 메소드로 웹 서버 객체를 만든다.
  - parameter로 요청에 대한 콜백 함수를 전달
  - 생성된 서버는 몇 가지 이벤트를 가지는데, 대표적으로 3가지 이벤트는: 
    - connection: 클라이언트와 서버 간의 연결 이벤트
    - request: 클라이언트로부터 서버로 http 요청 발생
    - close: 서버 종료 이벤트
  
  - request 이벤트가 발생하면 콜백 함수를 호출하며 request 객체와 response 객체가 파라미터로서 전달된다.
    - request 객체는 클라이언트의 요청에 관한 정보를 담고 있다.
    - response 객체는 서버의 응답에 대한 정보를 담고 있다.
    
  
 ```js
 const server = http.createServer((request, response) => {
  // 응답 내용
 })
 ```
 
 <br>
 
 - request 객체는 바이트 데이터를 읽을 수 있는 ReadableStream 인터페이스를 구현하고 있으며, 이 스트림에 
 
