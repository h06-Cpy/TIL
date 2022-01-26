# Heap
우선순위 기반 Queue로, 우선순위(크기)가 가장 높은 노드부터 out

properties

- heap-shape property: complete BT로, 마지막 depth는 left packing
- heap order property: 부모노드 값이 자식보다 크다. sibling은 상관 없음

array로 구현하며 다음과 같은 성질이 있음

- 0번째는 노드 개수, 1번째부터 데이터 들감
- 2i→left child, 2i+1→right child, floor(i/2)→parent
- internal node 개수 = floor(n/2), leaf node 개수 = n-floor(n/2)

array에 빈칸없이 연속적으로 데이터가 모여있으므로 shape property 유지 가능

## operation

**make-heap**: heap order property가 깨진 곳에서 부모 노드와 max(left, right)를 바꾸고  내려간 부모노드에서 다시 make-heap한다. O(log N) make-heap으로는 12345같은 배열을 힙으로 못만든다 → build-heap

**insert**: 일단 array 맨끝에 넣고 부모노드와 비교하여 삽입된 애가 크면 계속 올라간다. O(log N)

**delete**: root를 제거하고 그 자리에 맨 마지막 노드를 올린다. 새로운 root부터 make-heap한다. O(log N)

**build-heap**: 임의의 array를 힙으로 만든다. 방법 2가지

- 빈 heap에 하나씩 insert → insert를 n번하므로 O(nlogn)
- array 맨끝부터 root까지 make-heap O(n)
