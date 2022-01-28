# Sorting
정렬: 정수로 이루어진 리스트를 오름차순으로 정리하는 것

왜 함? 어떤 데이터의 위치를 대략적으로 알기 좋고 무엇보다도 **이진탐색** 쓸 수 있다!

정렬 알고리즘 평가 항목

- 효율성: 시간 복잡도가 얼마냐
- 어떤 연산 사용? - 대부분 비교 연산 사용
- 메모리 얼마나 사용? - n개 size 이상의 메모리를 ‘안’ 사용하면 **in-place**라고 함
- 안정성: 같은 숫자가 있을 때 정렬 후 순서가 안바뀌면 **stable**이라고 함

## Bubble Sort

**쓰지 마시오** 가장 간단하지만 가장 비효율적임

맨 뒤부터 시작해서 옆에 있는 애랑 비교해서 작은 놈을 앞에, 큰 놈을 뒤로 보냄

k번째 사이클에 k번째 작은 놈을 고르게 됨

O(n^2), in-place, stable

## Selection Sort

bubble을 개선해서 swap 개수를 줄임

k번째 사이클에 k번째 작은 놈을 골라 k-1번째 애랑 자리 바꿈

O(n^2), in-place, unstable

## Insertion Sort

정렬된 부분과 안된 부분 나누고 안된 부분에서 하나를 정렬된 부분에 넣는 방식

k번째 사이클에 k-1번째 원소를 정렬된 부분에 넣는다(비교하면서 계속 swap)

O(n^2), in-place, stable

## Shell Sort

gap이 있는 insertion sort

n/2의 gap만큼 떨어져 있는 원소들끼리(gap만큼 떨어져 있는 원소들이 sublist가 되는것임) 정렬 후 gap을 줄여나가면서 정렬

list의 처음부터 시작해서 gap만큼 떨어진 애랑 비교, 그다음 +1번째 원소도 gap만큼 떨어진 애랑 비교...

O(n^2), in-place, unstable

## Heap Sort

array에 원소들을 하나 하나 heap insert 쭉 해서 힙을 만들고 delete 쭉 해서 empty 힙을 만들면 정렬됨

delete할 때 힙에서 제거되는 애는 array의 뒤쪽으로 감

O(nlogn), in-place, unstable

## Merge Sort

divide and conquer 방식

1. 똑같은 크기의 두 부분으로 split
2. 각 부분을 sort
3. 인접한 두 부분을 merge하면서 sort

1~3을 재귀함수로 반복!

linked list 방식: 인접한 두 부분의 시작부터 각각 포인터를 만들고 포인터가 가리키는 원소끼리 비교해서 작은놈을 앞으로 땡겨서 insert하고 작은놈 가리키던 포인터가 그다음 원소를 가리킴

array 방식: 새로운 array를 만들고 linked list와 같이 포인터 두개로 비교해서 작은 놈을 새로운 array에 넣음

O(nlogn), in-place(linked list), not in-place(array), stable

그냥 반으로 나누기보다 더 좋은 건 없나?

## Quick Sort

pivot 원소를 정해서 그것보다 작은 거 큰 거 두 부분으로 나눠서 정렬

역시 재귀함수 이용해서 각 sublist에서도 pivot 정해서 나눔

worst: O(n^2)

best, average: O(nlogn)

in-place, unstable

## Radix Sort

십진수의 자리수마다 정렬

자릿수만큼 hash table 필요

1의 자리에서 hash table에 정렬된 순서로 대응(chaining 방식) ex) hash table 2에 12 -> 22 -> 92 chanining, 5에 35 -> 75 -> 85 chanining...
그 순서대로 다시 10의 자리, 100 자리... 이렇게 정렬

**Comparison이 없다!**

O(n), not in-place, stable
