---
title: <JS> stack, queue
layout: post
categories: [Data_Structure]
description: ""
customexcerpt: "JavaScript: Stack, queue"
comments: true
---

* hello
{:toc}


## stack ##
 - Last In, First Out : 나중에 들어온 것이 먼저 나간다. => 후입선출
 
  ![stack1](/assets/img/stack.png)
 
 <br>
 
 - stack property
 
  > top : 가장 최근의 요소의 인덱스(스택의 현재 위치/ 스택의 마지막 요소의 인덱스)
 
 - stack method
 
  > push(element) : 스택 끝에 요소를 추가
  
  > pop() : 가장 최근에 추가된 요소를 제거
  
  > size() : 스택의 크기를 반환
  
  > peek() : top의 요소를 반환
  
  > empty() : 스택에 요소가 있는지에 대해 불리안 값을 반환 // 빈 스택일 경우 1(true)
 
<br>

## JavaScript 객체를 이용한 Stack 메소드 구현 ##

- size(), push(), pop(), peek()

```js
class Stack {
  constructor() {
    this.storage = {};
    this.top = -1;
  }

  size() {
    return this.top + 1
  }

  push(element) {
    this.top ++
    this.storage[this.top] = element
  }

  pop() {
    if (this.top >= 0) {
      let poppedValue = this.storage[this.top]
      delete this.storage[this.top]
      this.top --
      return poppedValue
    }
  }
  
  peek() {
    return this.storage[this.top]
}

```
```js
let stack = new Stack()

stack.push('top0')
stack.push('top1')
// {storage: {0: "top0", 1: "top1"}, top: 1}

stack.size() // 2

stack.pop() // "top1"
```
<br>

## queue ##
 - First in, First out : 먼저 들어온 것이 먼저 나간다. => 선입선출

![queue](/assets/img/queue.png)

<br>

 - queue property
 
 > front : 첫 번째 요소의 위치
 
 > rear : 마지막 요소의 위치
 
 - queue method
 
 > enqueue(element) : queue 끝에 요소를 추가
 
 > dequeue() : 맨 앞의 요소를 제거
 
 > size() : 큐의 크기를 반환
 
 <br>
 
 ## JavaScript 객체를 이용한 Stack 메소드 구현 ##
 
 ```js
 class Queue {
  constructor() {
    this.storage = {};
    this.front = 0;
    this.rear = 0;
  }

  size() {
    return Object.keys(this.storage).length
  }

  enqueue(element) {
    this.storage[this.rear] = element
    this.rear ++
  }

  dequeue() {
    if (this.front <= this.size()) {
      let deQueueVal = this.storage[this.front]
      delete this.storage[this.front]
      this.front ++
      return deQueueVal
    }
  }
 }
 ```
 ```js
 let queue = new Queue()
 
 queue.enqueue('rear0')
 queue.enqueue('rear1')
 // {storage: {0: "rear0", 1: "rear1"}, front: 0, rear: 2}

 queue.size() // 2
 
 queue.dequeue() // "rear0"
 ```
