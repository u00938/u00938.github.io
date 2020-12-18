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
  - best case: 맨 끝(head/tail)에 삭제할 경우 O(1)
 
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

 - 배열은 연속적인, 순서가 있는 데이터 구조 / Linked list는 순서 없이 랜덤으로 위치한 노드들이 연결되어있는 데이터 구조
 - 배열은 인덱스로 원하는 데이터에 접근이 가능 / Linked list는 head부터 모든 노드를 탐색하여 원하는 데이터를 찾아야 한다.
 - 배열의 탐색 시간 복잡도 O(1) / Linked List 탐색 시간 복잡도 O(n)
 - 배열에서 요소를 삽입할 경우, 새로운 요소가 추가된 위치의 다음 요소들은 인덱스가 뒤로 1씩 shift되어야 하기 때문에 최악의 경우(인덱스 0번에 추가될 경우) O(n)의 시간 복잡도를 갖는다. / Linked List의 경우 삽입 시 O(1)의 시간 복잡도
 - 배열에서 요소를 삭제할 경우에도 삭제한 원소의 다음 요소들은 인덱스가 앞으로 1씩 shift되어야 하기 때문에 최악의 경우(인덱스 0번을 삭제할 경우) O(n)의 시간복잡도를 갖는다.
 - 배열은 고정된 크기를 가지고 있는 반면, Linked list는 동적인 크기를 가진다.
 - 배열은 데이터 자체를 저장하지만, Linked list는 데이터에 추가로 next(양방향의 경우 previous까지)를 가리키는 referencing element도 같이 저장되어야하기 때문에 메모리가 더 많이 사용된다.
 
<br>

## JS> Linked list 메소드 구현 ##

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this._size = 0;
  }

  addToTail(value) {
    const node = new Node(value)

    if (!this.head) {
      this.head = node;
      this.tail = node;
    }
    else {
      this.tail.next = node;
      this.tail = node
    }
    this._size ++;
  }

  remove(value) {
     const index = this.indexOf(value);
     
     if (index === -1) {
       return;
     }

     if (index === 0) {
       if (this.head === this.tail) {
         this.head = null;
         this.tail = null;
         this._size = 0;
       } else {
         this.head = this.head.next;
         this._size -= 1;
       }
       return;
     }

     const prevNode = this.getNodeAt(index - 1);
     const removedNode = prevNode.next;

     if (removedNode === this.tail) {
       prevNode.next = null;
       this.tail = prevNode;
       this._size -= 1;
       return;
     }

     prevNode.next = removedNode.next;
     this._size -= 1;
  }

  getNodeAt(index) {
    let current = this.head
    let count = 0;

    while (current) {
      if (count === index) {
        return current
      } 
      count ++
      current = current.next;
    }
    return undefined;
  }

  contains(value) {
  return this.indexOf(value) !== -1
  }

  indexOf(value) {
    let current = this.head
    let index = 0;

    while (current) {
      if (current.value === value) {
        return index
      }
      index ++
      current = current.next
    }
    return -1
  }

  size() {
    return this._size
  }
}
```

