# Set
뭔가 분류할 때 사용

집합 A와 B가 교집합이 없으면 mutually disjoint

**우리는 disjoint set을 이용하여 분류한다!**

트리의 root가 집합을 대표

원래 트리와 달리 모든 child는 root를 가리킴

## Operation

Find: 집합의 root를 리턴하는 함수, 어떤 원소를 인수로 받든지 집합의 parent를 리턴 O(N)인데 너무 큼!

Union: 두 집합을 하나로 만듦, 하나의 root가 다른 하나의 root를 가리키게 만듦 O(N)인데 너무 큼!

## Implementation

array로 구현

- array index = 노드의 값
- array 안의 값 = parent의 값
- array 안의 값이 0이면 root

## Operation 개선

Union 개선

- union by size: 노드 수가 작은 집합을 큰 집합 안에 넣음
    - array에서 root의 값을 0이 아니라 -size로 함
- union by height: 각 집합의 longest path length를 계산하여 작은 집합을 큰 집합 안에 넣음

O(logN)

Find 개선

path compression: 모든 노드가 root만을 가리키게 만듦 그럼 O(1)

근데 이건 union by height가 안됨 왜냐면 height가 사라져버림

그래서 union by rank 씀

rank: log2(size)
