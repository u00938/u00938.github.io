---
title: DOM - element 생성하기(createElement, createDocumentFragment)
layout: post
categories: [JavaScript]
description: ""
customexcerpt: "DOM - Create"
comments: true
---

* hello
{:toc}


## Document 객체 ##
- 웹 페이지 자체로서, 페이지 콘텐츠(tree구조)의 진입점
- 웹 페이지의 html 요소에 접근 하기 위해서는 document 객체를 통해야 한다.

## Document.createElement() ##
- html 요소를 만들어 반환하는 메소드. 태그를 지정할 수 있다.
- tag name을 인식할 수 없을 경우 HTMLUnknownElement를 반환한다.

```js
// div 태그 만들기
const newEl = document.createElement('div');

// 태그에 텍스트 추가하기
const textContent = document.createTextNode('엘리먼트를 생성합니다.'); 
newEl.appenChild(textContent); // 결과: <div>엘리먼트를 생성합니다.</div>
```

## Document.createDocumentFragment() ##
- 비어있는 새 DocumentFragment 생성
- DocumentFragment: 부모가 없는 document 객체로, 노드를 추가할 수 있는 임시 객체
- tree구조에 포함되지 않기 때문에 fragment를 변경해도 문서에는 영향을 미치지 않는다. // 가상의 노드 객체
- children을 추가할 때 브라우저 reflow가 일어나지 않는다. // better performance
- documentFragment 생성 -> element들을 documentFragment에 추가 -> documentFragment를 DOM tree에 추가



## 조회하기 ##
**document.body**
- 현재 문서의 <body> 노드 조회
- read-only
- 찾는 요소가 없을 경우 null 반환

**document.children**
- 자식 노드 조회
- ParentNode.children
- read-only

```js
// body의 1번째 자식 엘리먼트를 조회하기
let lookUpChild = document.body.children[1]

console.dir(lookupChild)
```
