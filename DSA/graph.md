# Graph
명제 증명, 블록체인에서도 쓰임 ㄷㄷ

## 정의와 종류

그래프 G는 집합 V(vertices)와 집합 E(edges)로 이루어져 있음

vertex: 값을 가지는 대상, 노드

edge: vertex를 연결하는 선

degree: 엣지 개수

loop: vertex쌍을 연결하는게 아니라 하나의 vertex에서 시작하고 끝나는 엣지

트리의 경우 |V|=|E|+1

그래프는 isomorphic(같은 그래프지만 모양은 다르게 보임) 가능

span: subgrapth가 모든 vertex, 일부분의 엣지를 가짐

spanning tree: subgrapth가 span할 때 edge수 최소

complete graph: 모든 vertex끼리 하나씩 엣지가 있음

multigraph: vertex pair중에 엣지 여러개 가지는게 있음

directed graph(digraph): 엣지가 방향을 가짐

weighted graph: 엣지가 weight(cost)를 가짐

## Path

path: 엣지로 연결되어 있는 인접한 vertices의 순서

simple path: 같은 경로(같은 엣지)를 또 지나는 경우 없음

elementary path: vertex를 또 방문하는 경우 없음

length: path에서 엣지 개수

cycle(circuit): legth가 1보다 크고 한 vertex에서 시작하고 끝나는 path

circuit도 simple, elementary 있음

## 연결
connected: 두 vertex 사이에 path가 있음

strongly connected: directed graph에서 a→b, b→a path 둘다 있음

connected component: 연결된 vertices의 모임

그래프 표현은 다음의 두가지 경우가 있음

- adjacency matrix: 엣지로 연결되면 1, 아니면 0을 정사각행렬로 표현
- adjacency list: 연결된 것을 hash table과 linked list로 표현

## Traversal

Traversal(순회, 탐색): 모든 vertex를 한번씩 방문하는 것

자료구조(스택, 큐)를 이용하여 방문 순서를 결정

BFS(Breadth-First Traversal): queue를 이용하여 순회

DFS(Depth-First Traversal): Stack을 이용하여 순회, 재귀함수를 이용할 경우 방문 표시를 나중에 함

adjacency matrix인 경우 O(V^2), list인 경우 O(V+E)

Modified recursive DFS: edge로 연결 안된 vertex도 방문 가능, 언제 들어가고 나왔는지 time도 표시하도록 개선

Topological Sort:
