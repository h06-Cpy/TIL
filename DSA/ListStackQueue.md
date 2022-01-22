주의! C언어 기준으로 작성
# List

리스트: 순서가 중요한 collection, 데이터의 모임!

array 구현

insert → 첫번째에 넣으면 옮겨야함, 마지막에 넣으면 거까지 가야함, 중간에 넣어도 마찬가지 O(N)

delete → 첫번째 없애면 옮겨야 함, 중간꺼 없애도 마찬가지 O(N)

### Linked List

포인터로 구현, head와 tail이 각각 첫번째와 마지막을 가리킨다.

 next만으로 연결하는 것이 기본, previous 있으면 이중연결리스트, 첫번째랑 마지막이 연결되면 원형연결리스트

insert → 첫번째 O(1) | k번째 O(k) | 마지막 tail 있으면 O(1) 아니면 O(N)

delete 마찬가지

이것은 next와 prev의 연결을 다시 해줘야 함! 연결할 때 문제생기지 않게 조심

access O(N)

# Stack

LIFO(Last In First Out), 그래서 가장 마지막에 들어온 놈을 가리키는 top이 존재

array, 연결리스트 구현 가능

push: top 다음에 새로운 애를 넣고 top을 새로 넣은 놈으로 함 O(1)

pop: 현재 top에 있는 놈을 빼고 그 아래에 있는 놈을 top으로 함 O(1)

# Queue

FIFO(First In First Out), head와 tail 존재

array, 연결리스트 구현 가능

Enqueue → tail에 삽입 O(1)

dequeue → head를 삭제 O(1)
