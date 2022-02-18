# P and NP
어떤 문제가 어렵다(hard)는 것은 빨리 못 푼다는 것

어렵다고 증명되면 더이상 빠른 알고리즘을 찾으려 노력 안해도 됨

그냥 좋은 approximate solution을 찾는데 시간을 쏟으면 됨

---

tractable: 어떤 문제의 솔루션이 O(n^k) 즉,  n의 polynomial의 복잡도를 가진 경우, 그 문제는 tractable하며 easy한 거임

지금까지 본 문제들은 모두 tractable

---

문제 유형

예를 들어 집합 {-2,-3,15,14,7,-10}의 부분 집합 중에 더해서 0되는 게 있냐는 문제

이것은 계산해야 하니까 computation(optimization) 문제지만

임의의 부분집합 골라서 0되나 안되나 확인하는 decision problem으로 바꿀 수 있음

---

P and NP 문제

class P에 있는 문제는 polynomial time으로 ‘풀 수 있는’ decision problems

class NP에 있는 문제는 polynomial time으로 솔루션들이 ‘검증될 수 있는’ 문제, 즉 검산이 쉬운 decision problems

문제는 **P와 NP가 같은 집합인가?**

아니면 P가 NP에 포함되어 있나?(NP인데 P는 아닌 문제가 있나?) 아직 증명 안됨

---

Reducibility: 문제 P가 문제 Q로 바뀔 수 있을 때 P는 reducible to Q

P가 Q보다 어렵진 않다는 것을 알 수 있음

NP-Hard: NP class에 있는 임의의 문제 P가 Q에 대해 reducible할 때 Q는 NP-Hard

NP-Complete: Q가 NP-Hard이고 Q도 NP class에 있는 문제일 경우

**NP-Complete 문제를 polynomial time으로 풀 수 있다면 모든 NP 문제들을 polynomial time으로 풀 수 있다!**

NP-Complete는 6개의 문제가 있는데 이것들을 풀 수 있다면 P=NP이고 아니면 P는 NP에 포함된다.

---

NP-Complete 문제들

- Hamiltonian Cycle: 그래프에서 각 vertex를 한번만 방문하는 cycle 찾기
- Longest path: 그래프에서 x→y로 가는 가장 긴 acyclic path 찾기
- Circuit satisfiability: AND, OR, NOT 게이트로 이루어진 논리회로에서 1이 출력되도록 입력의 조합을 찾을 수 있는가
- Partitioning: 어떤 정수 집합을 같은 합을 가지는 두 집합으로 나눌 수 있는가
- Graph Coloring: 각 엣지가 다른 색을 가진 vertex를 연결하도록 하는 최소의 색깔 개수를 구하는 문제
- Scheduling: 해결하는데 시간이 다 다양한 업무들의 집합이 있을 때 데드라인을 지키면서 업무들을 2개의 동일한 프로세서로 나눌 수 있는가
