---
title: DOM - element를 DOM 구조에 연결하기(append, appendChild, prepend)
layout: post
categories: [JavaScript]
description: ""
customexcerpt: "DOM - Append"
comments: true
---

* hello
{:toc}


## append ##
- parentNode.append()
- 부모 노드의 마지막 자식 뒤에, 즉 맨 끝에 노드 객체 또는 DOMString 객체를 삽입
- 여러 개 노드와 문자를 추가할 수 있다.
- rest parameter를 사용할 수 있다. // parentNode.append(...nodes);
- 반환하는 값이 없다.
- JavaScript 메소드로 확장성이 뛰어나다.
- IE(인터넷 익스플로러) 호환 안됨

## appendChild ##
- Node.appendChild()
- append와 같은 기능: 부모 노드의 자식 노드 맨 끝에 노드 삽입
- 오직 노드 객체만 추가 가능하다. (문자열 노드는 지원하지 않는다)
- 추가한 Node 객체를 반환한다.
- 하나의 노드만 추가할 수 있다. // 노드가 이미 존재할 경우 새로운 위치로 이동시킨다.
- DOM 메소드
- IE 호환

## append vs. appenChild ##
- append는 문자열을 바로 추가할 수 있다.

```js
// append: 문자열을 바로 추가
document.getElementById('userId').append('Hello!');

// appendChild: 텍스트 노드를 따로 만들어 변수에 저장한 후 parameter를 통해 불러온다.
const addText = document.createTextNode('Hello!');

document.getElementById('userId').appendChild(addText);
```

- append는 element와 text를 동시에 추가할 수 있다.

```js
const parentDiv = document.createElement('div');
const childP = document.createElement('p');

parentDiv.append("Add Text", p);
// document.body.append(parentDiv) 결과: div 태그 안에 'Add Text'와 p태그가 자식 엘리먼트로 추가되었다.
```

## prepend ##
- parentNode.prepend()
- 부모 노드의 첫 자식 노드 앞에, 즉 맨 앞에 노드 객체 또는 DOMString 객체를 삽입
- 여러 개 노드와 문자를 추가할 수 있다.
- rest parameter를 사용할 수 있다. // parentNode.prepend(...nodesToPrepend);
- 반환하는 값이 없다.
- JavaScript 메소드로 확장성이 뛰어나다.
- IE(인터넷 익스플로러) 호환 안됨

## append vs. prepend ##
- 객체를 삽입하는 위치만 다를 뿐 다른 특징은 동일하다.
- append는 자식노드 맨 끝에, prepend는 자식노드 맨 앞에 객체를 삽입한다.
