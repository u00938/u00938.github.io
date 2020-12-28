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
  
    ```js
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
 
 
