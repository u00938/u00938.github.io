---
title: Hash level1 - 완주하지 못한 선수
layout: post
categories: [Algorithm]
description: ""
customexcerpt: "Algorithm"
comments: true
---

* hello
{:toc}


## 문제 이해
[문제 보러 가기](https://programmers.co.kr/learn/courses/30/lessons/42576)
- 마라톤 참가자(participant)와 완주자(completion) 배열을 이용해 완주하지 못한 한 명의 선수를 찾는다.
- 동명이인이 있을 수 있다.

<br>

## 풀이 1
처음 생각한 것은 완주자 배열을 모두 돌면서 참가자 내에서 인덱스를 찾아서, 참가자 목록에서 지워나가고 마지막 남는 참가자를 리턴하는 것이었다.
정확성 테스트는 모두 통과하였으나 효율에서 모두 틀렸다.

for문으로 인해 이미 O(n)의 시간 복잡도가 드는데, indexOf에서도 O(n)의 시간이 쓰이다보니 효율 면에서 구릴 수밖에😅🤯

```js
function solution(participant, completion) {
  for (let i = 0; i < completion.length; i++) {
    const index = participant.indexOf(completion[i])
    participant.splice(index, 1)
  }
  return participant.toString();
}
```

<br>

## 풀이 2
그렇다면 for문과 같은 O(n)은 한 번으로 줄여야 한다. 여기서 나온게 둘 모두 정렬을 해서, 같은 인덱스를 비교하고 같은 자리에 다른 값일 경우 그 놈이 범인인걸로!

정확성, 효율성 테스트 모두 통과되었다.

```js
function solution(participant, completion) {
  participant.sort()
  completion.sort()
  for (let i = 0; i < participant.length; i++) {
    if (participant[i] !== completion[i]) {
      return participant[i];
    }
  }
}
```

<br>

## 풀이 3
그런데 다른 사람의 풀이에서.. 정말 까리한 코드를 발견했다. 

처음에는 이해하기 어려운 한 줄 코드였으나, 이건 고수들의 코드이고 내 수준 맞춤으로 다시 써보기로 했다.

```js
const solution = (participant, completion) => {
  completion.map(name => completion[name] = (completion[name] | 0) + 1)
  return participant.find(name => !completion[name]--)
}
```

<br>

완주자 배열을 맵핑하여 각 이름과 갯수를 키-밸류로 배열의 요소에 추가한다.

예를 들면 배열 ["a", "b", "c"] 맵핑의 결과는 ["a", "b", "c", a: 1, b: 1, c: 1] 가 될 것이다.

전체 참가자의 배열이 ["a", "b", "c", "d"] 일 때, 참가자 이름을 하나씩 돌면서 이렇게 맵핑된 완주자 배열에서 이름과 값을 확인한다.

find 메소드는 첫번째 true인 값을 리턴하는 함수이다.

만약 밸류가 1인 경우 true이므로 !completion[name]은 반대인 false 값이 되어 다음 요소를 확인하는데, 이 때 밸류를 하나씩 빼준 다음, 즉 밸류값을 0으로 내리고 다음 값으로 이동한다. 

만약 이 때 참가자 중 동명이인이 있을 경우 같은 이름에 대한 밸류는 이미 0이 된 상태이기 때문에 falsy한 값을 가지며, ! 연산자에 의해 반대인 true로 인지되어 해당 이름이 리턴되게 될 것이다.

만약 완주자 배열에 없는 참가자 이름을 확인할 경우 completion[name]의 밸류는 undefined이며 이는 fasly하고, ! 연산자에 의해 true한 값이 되어 해당 이름이 리턴된다. 참고로 undefined 밸류에서 -- 연산이 되면 해당 이름은 NaN으로 들어간다. 즉, ["a", "b", "c", a: 1, b: 1, c: 1, d: NaN]

위의 코드를 한 줄로 정리할 수도 있다.

```js
const solution = (participant, completion) => participant.find(name => !completion[name]--, completion.map(name => completion[name] = (completion[name] | 0) + 1))
```

find에 두 개의 파라미터가 들어가는데, 두 번째 인자로 map 함수가 들어갔다.

find 메소드의 두 번째 인자는 thisArg 자리이며 선택적으로 사용되는데, mdn에서는 이를 "콜백이 호출될 때 this 로 사용할 객체" 라고 설명한다.

즉 첫번째 인자의 콜백이 실행되기 전에 먼저 실행 및 정의가 된다는 뜻이다!

이를 이용한 아주 똑똑한 풀이 방식이었다.

그런데 한 줄로 끝낸다는 것이 멋있어 보이긴 하지만, 개인적으론 가독성이 너무 떨어지는 것 같다.

그래서 이해하기 힘들긴 했지만 역시 봐도 봐도 간지난다💦

