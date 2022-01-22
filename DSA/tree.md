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

search하려면 traverse해야 한다. 근데 만약 skewed tree이면 O(N)이다.

너무 길어! 만약 이진탐색처럼 O(logN) 안될까? →BST

## Binary Search Tree(BST)

한 노드가 있으면 노드의 값이 left subtree의 값보다 크고 right subtree의 값보다는 작다.

inorder traversal하면 정렬된 숫자리스트이다.
