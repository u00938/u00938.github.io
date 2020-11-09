---
title: JavaScript 배열 내장 고차함수: forEach, find, filter, map, reduce, sort, some, every
layout: post
categories: [JavaScript]
description: ""
customexcerpt: "JavaScript: array method "
comments: true
---

* hello
{:toc}

## 기본 개념 정리
- 자바스크립트의 함수는:
  1. 변수에 할당(assignment)될 수 있다. 
  2. 다른 함수의 인자(argument)로 전달될 수 있다.
  3. 다른 함수의 결과로서 return 될 수 있다
- 고차 함수(higher order function): 함수를 인자(argument)로 받거나 함수를 return하는 함수
- 콜백 함수(callback function): 다른 함수(caller)의 인자로 전달되는 함수. caller는 콜백 함수를 호출(invoke)하고 조건에 따라 실행하거나 여러 번 실행할 수 있다.
- 커리 함수(curry functon): 함수를 리턴하는 함수

## forEach: 단순 반복

```js
const fruits = ['apple', 'banana', 'mango'];

// 사용법1: 기본(호출)
// element는 배열의 요소
const getEach = function(element) {
  console.log(element);
}
fruits.forEach(getEach) // 결과: 'apple', 'banana', 'mango'

// 사용법2: 콜백 함수를 사용(function(fruit)는 콜백함수로 forEach 함수에 인자로서 전달되었다.
fruits.forEach(function(fruit) {
  console.log(fruit); // 결과: 'apple', 'banana', 'mango'
})
```


## find: 조건 함수를 만족하는 첫 번째 요소의 값
- 조건을 만족하는 첫 번째 값만을 반환하고 바로 종료된다.
```js
const students = [
  { name: 'Harry', age: 15 },
  { name: 'Ron', age: 14 },
  { name: 'Hermione', age: 14 },
];

const findRon = students.find(function(element) {
  return element.name === 'Ron';
})
console.log(findRon); // 결과: {name: "Ron", age: 14}
```


## filter: 조건 함수를 만족하는 모든 요소로 새로운 배열을 생성
```js
const students = [
  { name: 'Harry', age: 15 },
  { name: 'Ron', age: 14 },
  { name: 'Hermione', age: 14 },
];

const onlyFourteen = students.filter(function(element) {
  return element.age === 14; // 조건
})
console.log(onlyFemale); // 결과: [{ name: 'Ron', age: 14 }, { name: 'Hermione', age: 14 }]
```


## map: 모든 요소들이 함수에서 리턴된 결과값들로 구성된 새로운 배열 생성
- 추후 업데이트 . . .
