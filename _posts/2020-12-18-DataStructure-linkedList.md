---
title: <JS> Linked List
layout: post
categories: [Data_Structure]
description: ""
customexcerpt: "JavaScript: Linked List"
comments: true
---

* hello
{:toc}


## Linked List ##
 - 비연속적인(non-contiguous) 데이터 구조
 - 데이터를 담고 있는 node가 메모리 상에 랜덤으로 위치해 있으며, 동시에 다음 node를 가리키는 link를 가지고 있다.
 - 각 노드는 데이터 + 다음 노드를 가리키는 link로 구성된다.
 
  ![linkedlist](/assets/img/ll.png)
  
 <br>
 
## Time Complexity ##



 **탐색**
  - head부터 next link를 통해 모든 노드를 탐색해야하므로 최악의 경우 O(n)의 시간 복잡도를 갖는다.
  
  ![linkedlist](/assets/img/ll2.png)
  
<br>
  
 **노드 삽입**
 
   
  ![linkedlist](/assets/img/ll4.png)
 
  - 추가할 위치(앞 노드의 위치)를 알고 있다고 가정한다.
  - 노드를 추가할 위치에서 기존 링크를 끊은 후 이전 노드의 링크와 삽입할 노드를 연결, 삽입할 노드의 next link를 다음 노드와 연결하면 된다.
  - 추가할 노드를 앞 노드, 다음 노드와 연결하기만 하면 되므로 O(1)의 시간복잡도를 갖는다.
  
  <br>
 
 **노드 삭제**
 
   
  ![linkedlist](/assets/img/ll5.png)
 
  - 삭제할 노드의 이전 노드의 next link가 삭제 노드 next 노드와 연결되게 한다.
  - worst case: 삭제하려는 위치를 찾기 위해 처음부터 탐색해야하므로 최악의 경우 O(n)의 시간 복잡도가 든다.
  - best case: 맨 끝(head/tail)에 추가/삭제할 경우 O(1)
 
<br>
 
## Doubly linked list ##
 - 양방향 연결 리스트(doubly linked list)는 다음 노드를 연결하는 링크만 가지는 단순 연결 리스트(singly linked list)와 다르게 해당 노드가 이전 노드를 연결하는 링크과 다음 노드를 연결하는 링크를 가지고 있다.
 - 양방향으로 연결되어 있기 때문에 양방향으로 노드를 탐색할 수 있다.

 ![linkedlist](/assets/img/doublell.png)

<br>

 - 삽입의 시간 복잡도는 O(1), 탐색의 시간 복잡도는 O(n)
 - 삭제 시 이전 노드의 주소를 알 수 있으므로 이전 노드와 해당 노드 사이의 링크만 끊어주면 접근이 불가하게 되어 삭제된다. 따라서 단방향 연결 리스트와는 다르게 삭제에서 O(1)의 시간 복잡도를 갖는다.
 - 중간 지점 이전의 노드는 head 노드부터 next link를 이용해 조회하고, 중간 지점 이후의 노드는 tail 노드부터 previous link를 이용해 조회한다.
 - 이러한 양방향 탐색은 최악의 경우 노드 전체를 탐색해야하는 단순 연결 리스트에 비해 탐색할 엘리먼트가 반으로 줄어든다.
 - 대신 양방향 연결 리스트는 이전 노드를 지정하기 위한 변수를 위해 메모리를 더 많이 차지하고 구현이 복잡하다.

<br>

## Array vs.Linked List ##


