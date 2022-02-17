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

자료구조(스택, 큐)에다가 vertex를 넣고 뺴면서 방문 순서를 결정

BFS(Breadth-First Traversal): queue를 이용하여 순회

DFS(Depth-First Traversal): Stack을 이용하여 순회

DFS with recursive: 재귀함수는 시스템 스택을 이용, 인접한 애들 먼저 방문부터하고 방문했다는 표시를 나중에 함

adjacency matrix인 경우 O(V^2), list인 경우 O(V+E)

---

**Modified recursive DFS(mDFS)**: edge로 연결 안된 vertex도 방문 가능, 언제 들어가고 나왔는지 time도 표시하도록 개선

Topological Sort: DAG(directed acyclic graph)를 정렬하는 방법, mDFS를 이용하여 vertex에서 빨리 나간 순서대로 연결리스트 맨앞으로 보내면 critical path를 찾을 수 있음, O(V+E)

## Connected Component

directed graph에서 strongly connected component(SCC) 찾기 O(V+E)

1. mDFS(G) 호출해서 vertex나간 시간 계산
2. mDFS(G^T) 호출하는데 나간 시간 내림차순으로 방문 (G^T는 엣지 방향 바꾼거)
3. 그러면 G^T에서 엣지 방향대로 가다가 더이상 방문할 곳이 없으면 내림차순으로 다른 vertex에 방문할 것임 이런 끊김이 발생하면 이전 vertex까지 SCC임

---

undirected graph에서 connected component(CC) 찾기 O(E logV)

1. 모든 vertex를 독립된 set으로 초기화
2. 모든 엣지도 연결된 vertex들을 union함
3. 그러면 find했을 때 같은 vertex가 나오면 CC이고 아니면 CC 아님

## Shortest Path Algorithm
엣지에는 weight(cost)가 있으며 weight합이 가장 작은 path, 즉 SP를 찾는 것이 문제

SP problem 종류

- single source SP: 한 vertex에서 다른 모든 vertex로 갈때 SP(시작점만 정해짐)
- single destination SP: 한 vertex로 갈떄 SP (도착점만 정해짐)
- single pair SP: 시작점과 도착점이 정해짐
- all pair SP 모든 vertex 쌍에 대해 SP

**edge relaxation**: SP를 이루는 모든 subpath는 최소의 weight를 가짐

---

single source SP부터 알아보자, 여기에는 다익스트라, 벨만포드가 쓰임

Dijkstra, Bellman Ford 두가지 알고리즘 다 edge relaxation 기반으로 함

### Dijkstra’s Algorithm

가정

- connected graph
- edge weight는 음수가 없어야 함

 SP 못 찾은 집합에서 하나를 SP 찾은 집합에 들이는 알고리즘

과정

1. SP 집합 S와 못찾은 집합 V-S를 찾기
2. weight가 가장 작은 u(V-S에 있음)를 찾음
3. u를 S에 편입시킴
4. V-S가 empty될 떄까지 1~3 반복

O(V^2+E), 만약 heap을 사용하면 O(V+E)logV

음수 값에서는 다익스트라 적용안됨 → 벨만포드

### Bellman-Ford’s Algorithm

음수를 포함한 cycle에서는 적용 안됨, 음수 사이클을 찾으면 false 리턴함

다익스트라는 한번 구한 path에서 다시 weight를 계산하지 않지만 벨만포드는 다시 계산함

음수 weight가 있으면 최소 weight가 바뀌기 때문

O(V*E)

---

all pair SP 문제도 알아보자, 여기에는 플로이드 와셜 알고리즘이 쓰임

weight를 정사각행렬로 표현(directed graph니까 출발→도착 표현 가능)

행은 시작 노드, 열은 도착 노드임

### Floyd-Warshall’s Algorithm

SP를 찾을 때 한 vertex를 경유하는게 빠른가? → 정사각행렬에서 weight 값 수정

아닌가? → wieght값 그대로 놔두기

이렇게 해서 한 vertex를 경유하는 것부터 모든 vertex를 경유하는 경로까지 모두 비교함

경유하는 vertex에 해당하는 행은 weight가 무조건 고정

O(V^3)

## Minimum Spanning Tree Algorithm(MST)

MST: 최소 weight(cost)의 spanning tree

### Prim’s Algorithm

다익스트라랑 비슷하게 집합 V-S에 있는 원소를 S로 편입시키는 것임

편입시키는 기준은 인접한 엣지 중 cost 최소

cost 최소인게 2개 이상이면 random하게 고르거나 vertex값 작은거 고름

O(V^2), heap 사용 시 O((V+E)logV)

### Kruskal’s Algorithm

인접한 vertex에서 고르는 프림과 달리 크루스칼은 cost 최소인 엣지 자체를 고름

엣지를 고를 때 사이클을 만들지 않아야 함

O(ElogE)

## Maximum Flow Algorithm
directed graph에서 source → sink로 가는 최대 flow 값을 구하는 것이 문제

residual network: capacity - flow를 연산해서 완전 양수인 net flow만 계산

path augmenting: residual network로 부터 만들어진 simple path

### Ford-Fulkerson Algorithm

source → sink로 가는 simple path를 찾고 최소 flow를 기준으로 path augmentation 함

simple path를 못찾을때까지 하면 지금까지 기준으로 했던 최소 flow들의 합을 구하면 그것이 maximum flow임

f가 maximum flow일 때 O(f*E)
