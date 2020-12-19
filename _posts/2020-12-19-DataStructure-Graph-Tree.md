---
title: <JS> Graph, Tree
layout: post
categories: [Data_Structure]
description: ""
customexcerpt: "JavaScript: Graph, Tree"
comments: true
---

* hello
{:toc}


## Graph ##

  ![graph](/assets/img/graph1.png)

 - 노드(vertex, N) + 노드와 노드를 연결하는 간선(edge, E)으로 구성되는 비선형 자료구조
 - 인접 정점(adjacent vertex): 간선에 의해 연결된 정점(노드 A, B)
 - 방향성에 따라 무방향 그래프와 방향 그래프로 구분된다.
 - 무방향 그래프(undirected graph): 방향이 없기 때문에 두 개의 노드만 존재할 경우 두 노드는 서로 대칭이다.(A-B)
    - 차수(degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수(노드 B의 차수는 3)
  
 - 방향 그래프(directed graph): 방향성을 가지기 때문에 2개의 노드만 존재할 경우 두 노드는 비대칭 관계이다.(A->B)
    - 진입 차수(in-degree): 외부 노드에서 들어오는 간선의 수
    - 진출 차수(out-degree): 한 노드에서 외부로 향하는 간선의 수
    
 - 단순 경로(simple-path): 경로 중 반복되는 정점이 없는, 같은 간선을 두 번 이상 지나가지 않는 경로
 
## Graph 구현 방식 ##
 **1. 인접 리스트(Adjacency List)**

![graph](/assets/img/graph3.png)

  - 가장 일반적인 방법
  - 각 정점에 인접한 정점들을 인접 리스트에 저장/표시
  - 연결된 간선의 정보만을 저장하기 때문에 O(E)의 공간만 차지하므로 공간 효율성이 좋다.
 
 <br>
 
 **2. 인접 행렬(Adjacency Matrix)** 
 
![graph](/assets/img/graph2.png)
 
  - 정점들을 이차원 배열을 이용해 구현하는 방식
  - 인접 정점일 경우 1/ 아닐 경우 0
  - 간선의 수와 무관하게 항상 n^2 만큼의 메모리 공간을 차지한다.
  - 특정 노드의 인접 노드를 탐색하기 위해서는 모든 노드를 전부 순회해야 한다. 
  
  ```js
  if (노드 i, j를 잇는 간선이 그래프에 존재) {
    matrix[i][j] = 1;
  else {
    matrix[i][j] = 0;
  }
  ```

<br>

## 그래프의 탐색 ##

 **DFS(깊이 우선 탐색, Depth-First Search)**
  - root에서 시작하여 다음 branch로 넘어가기 전에 해당 분기를 완벽하게 탐색
  - 미로 탐색: 한 방향으로 갈 수 있을 때까지 가다가, 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아가서 다른 방향으로 다시 진행 탐색
  - 넓게(wide) 탐색하기 전에 깊게(deep) 탐색
  - 모든 노드를 방문하고자 하는 경우 사용하는 탐색법
  - 자기 자신을 호출하는 순환 알고리즘
  - 어떤 노드를 방문했었는지 여부를 반드시 검사해야 함 -> 무한루프에 빠지지 않기 위함
  - Stack을 사용하여 방문한 노드들을 스택에 저장했다가 꺼내며 탐색(후입선출//LIFO)
  
  ```js
  let visited; // 탐색을 마친 노드를 넣을 배열
  let needVisit; // 탐색해야 할 노드들이 들어있는 배열
  node = needVisit.shift()
  visited.push(node)
  ```
  
  - DFS의 시간 복잡도
    - 모든 간선을 조회
    - 인접 리스트 그래프: O(N + E)
    - 인접 행렬 그래프: O(N^2)

  - Backtracking: 조건에 유효하지 않으면 배제 후 부모 노드로 되돌아가는 문제 풀이 전략

  **BFS(너비 우선 탐색, Breadth-First Search)**
  - root에서 시작하여 인접한 노드를 먼저 탐색
  - 시작 정점으로부터 가까운 정점을 먼저 방문
  - 깊게(deep) 탐색하기 전에 넓게(wide) 탐색
  - 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을때 사용하는 탐색법
  - 사람 A와 B 사이의 친구 관계 경로 찾기
    - DFS: 모든 친구 관계를 다 살펴봐야 함
    - BFS: A와 가까운 관계부터 탐색
  
  - 재귀적으로 동작하지 않는다.
  - 마찬가지로 어떤 노드를 방문했었는지 여부를 반드시 검사
  - 큐를 이용하여 방문한 노드들을 차례로 저장 후 꺼내며 탐색(선입선출//FIFO)

<br>

## JS> Graph 메소드 구현 ##

```js
// 무방향 그래프
class Graph {
  constructor() {
    this.nodes = {};
  }

  addNode(node) {
    this.nodes[node] = this.nodes[node] || [];
  }

  contains(node) {
    return Boolean(this.nodes[node])
  }

  removeNode(node) {
    if (this.contains(node)) {
      delete this.nodes[node]
    }
  }

  hasEdge(fromNode, toNode) {
    if (this.contains(fromNode) && this.contains(toNode)) {
      if (this.nodes[fromNode].includes(toNode) && this.nodes[toNode].includes(fromNode))
        return true;
    }
    return false;
  }

  addEdge(fromNode, toNode) {
    this.nodes[fromNode].push(toNode)
    this.nodes[toNode].push(fromNode)
  }

  removeEdge(fromNode, toNode) {
    if (this.contains(fromNode) && this.contains(toNode)) {
      if (this.hasEdge(fromNode, toNode)) {
        const toInFromIdx = this.nodes[fromNode].indexOf(toNode)
        const fromInToIdx = this.nodes[toNode].indexOf(fromNode)
        this.nodes[fromNode].splice(toInFromIdx, 1)
        this.nodes[toNode].splice(fromInToIdx, 1)
      }
    }
  }
}
```
