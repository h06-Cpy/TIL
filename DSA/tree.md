# Tree
데이터 저장하는 node, node를 연결해주는 선 edge로 구성

계층구조를 가지고 있고 가장 꼭대기는 root라고 함

자식 노드가 없으면 leaf node, 안에 있으면 internal node

**모든 노드의 쌍은 오직 하나의 엣지만 가지고 있어야 한다**

acyclic graph이다.

root → depth 0부터 해서 자식 노드로 갈수록 하나씩 +1 된다

## Binary Tree(BT)

childern이 최대 2개인 tree, 가장 유용하다

정확한 정의: empty이거나 root에서부터 left, right subtree를 가지고 있는 tree

full BT: leaf는 자식노드 없고 나머지는 모두 2개 자식노드 있음

complete BT: depth n-1 까지는 full이고 depth n은 왼쪽부터 left packing

balanced BT: left와 right subtree의 height 차이 ≤1

## traversing

preorder: node → left → right

inorder: left → node → right

postorder: left → right → node

search하려면 traverse해야 한다. 

sequential search는 O(N)이다. 너무 느리다! 만약 이진탐색처럼 O(logN) 안될까? → BST

## Binary Search Tree(BST)

한 노드가 있으면 노드의 값(키)이 left subtree의 값보다 크고 right subtree의 값보다는 작다.

inorder traversal하면 정렬된 숫자리스트이다.

BST 가능한 모양
- Full
- Balanced
- skewed tree(일자로 쭉)

Insert: 삽입할 노드를 계속 비교하면서 내려감 leaf 노드에서 왼쪽 또는 오른쪽에 삽입 O(height)

**delete**는 삭제할 노드의 자식 수에 따라 3가지 경우가 있다. O(height)
- leaf 노드 삭제(자식 수 0): 그냥 그거 삭제
- 자식 하나: 자식 노드를 부모 노드랑 연결 시키고 삭제
- 자식 둘: inorder 상 자기 다음 노드(inorder successor)를 자기 위치로 옮겨서 부모 노드랑 연결시키고 삭제, 자기 다음 노드가 원래 있던 자리에서 다시 delete operation 수행

operation을 보면 다 height에 복잡도 비례한다.

skewed tree면 O(N)이 되어버리기 때문에 O(logN)이라는 원래 목적 달성이 안된다. balanced tree이면 좋을텐데! -> AVL tree

## AVL Tree

BST 중에서 left랑 right subtree의 height 차가 1 이내인 것

Balanced factor(BF) = left height - right height

AVL tree에서 정의에 의하면 BF는 -1, 0, 1 중에 하나만 나와야겠죠?

Insert는 두가지 rotation을 통해 특성을 유지(unbalance가 생길때 youngest ancestor 기준)
- 바깥쪽에 삽입된 경우: 2번째 youngest ancestor를 youngest ancestor에게 자식 하나 주면서 올림(single rotaion)
- 안쪽에 삽입된 경우: 3번째를 2번째로 rotaion 후 다시 3번째를 1번째로 rotation(double rotaion)

**delete:** insert랑 똑같이 bf 문제 없으면 걍 삭제, single, double rotation

복잡도: 모든 operation O(log2 N)

## B Tree

m-ary search tree이다.

root는 leaf거나 적어도 2개 자식을 가짐

internal 노드는 ceil(m/2) ~ m개의 자식 가지고 m-1개 key를 가짐

모든 leaf 노드는 같은 depth를 가지며 ceil(m/2)-1 ~ m-1개의 key를 가짐

예) 3-ary B tree 또는 2-3 tree

O(log m n) block access

insert는 splitting을 하며 두가지 경우가 있다

- leaf node: data 수 > m-1 이면 두개 leaf로 split
- nonleaf node: 자식 수 > m이면 두개 internal node로 split

delete는 borrowing과 merging을 하며 두가지 경우가 있다

- leaf: data 수 < m/2-1이면 sibling leaf랑 borrow와 merge
- nonleaf: 자식 수 < m/2이면 sibling internal node랑 borrow와 merge

B 트리는 70% 메모리를 사용한다.

B* 트리는 잘 안쓰이며 ceil(2m/3) ~ m이다.

B+ 트리는 leaf노드를 연결하여 sequential access가 가능하다.
