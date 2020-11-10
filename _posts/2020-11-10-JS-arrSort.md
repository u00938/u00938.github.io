---
title: JavaScript 배열 정렬하기 - sort()
layout: post
categories: [JavaScript]
description: ""
customexcerpt: "JavaScript: sort"
comments: true
---

* hello
{:toc}

## Array.sort(): 배열의 요소를 정렬한 배열을 반환 ##
- 복사본이 아닌 원 배열이 정렬된다.
- 요소를 문자열로 변환하여 오름차순 정렬한다.

```js
// 기본적인 방법 1. 문자열 정렬
const colors = ['red', 'blue', 'orange']

const sortColors = colors.sort();
console.log(sortColors); // 결과: ['blue', 'orange', 'red']

// 기본적인 방법 2. 숫자 정렬: 문자열로 변환되어 오름차순 정렬된다.
const numbers = [1, 14, 100000, 5, 32];

const sortNums = numbers.sort();
console.log(sortNums); // 결과: [1, 100000, 14, 32, 5]
```

## 매개변수 compareFunction ##
- 숫자를 크기대로 정렬하거나 원하는 방향으로 정렬하기 위해 정렬 기준 역할을 하는 함수를 매개변수로 전달한다.
- compareFunction: 요소를 비교해서 정렬 순서를 정의하는 함수. 생략하면 요소를 문자열로 변환하고 오름차순 정렬
- compareFunction(a, b): a와 b는 비교되는 두 요소
- a < b 일 경우 -1 반환 => 순서가 바뀌어 b가 a보다 먼저 나오게 된다.
- a = b 일 경우 0 반환 => 순서를 바꾸지 않는다.
- a > b 일 경우 +1 반환 => a가 이미 앞에 있기 때문에 순서를 바꾸지 않는다.

```js
function compare(a, b) {
  if (어떤 기준에 의해 a가 b보다 작은 경우) {
    return -1;
  }
  if (어떤 기준에 의해 a가 b보다 큰 경우) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

- 숫자를 비교하기 위해서 a - b 를 전달(오름차순)
- a와 b를 비교하면서 a > b 이면 양수, a < b 이면 음수, a = b 이면 0 을 반환하면서, 이 값에 따라 순서가 바뀌거나 바뀌지 않는다.

```js
const numbers = [1, 14, 100000, 5, 32];

const sortNums = numbers.sort(function(a, b) {
  return a - b;
});
console.log(sortNums); // 결과: [1, 5, 14, 32, 100000]
```


- 배열 내 객체의 한 속성 값을 기준으로 정렬할 수도 있다.

```js
const items = [
  { name: 'Yogurt', cost: 21 },
  { name: 'Apple', cost: 37 },
  { name: 'Milk', cost: 20 },
  { name: 'Eggs', cost: 12 },
  { name: 'Snack', cost: 13 },
];

// cost 기준으로 정렬하는 함수
items.sort(function (a, b) {
  if (a.cost > b.cost) {
    return 1;
  }
  if (a.cost < b.cost) {
    return -1;
  }
  return 0; // a와 b가 같을 경우
});

// 결과: [{ name: 'Eggs', cost: 12 }, { name: 'Snack', cost: 13 }, { name: 'Milk', cost: 20 }, { name: 'Yogurt', cost: 21 }, { name: 'Apple', cost: 37 }] 
```




