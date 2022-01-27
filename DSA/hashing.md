# Hashing
## 왜 만듦?

시간복잡도 O(1)인 자료구조 필요!

array가 있는데?

array는 size를 미리 정해야 함. 근데 얼마나 필요할지 몰라서 크게 정함 ex) 99999999개 저장

그러면 size가 작을 때 메모리 낭비 너무 심함

**메모리를 작게 사용하면서 O(1)에 가깝게 만들기!**

## 구성

- hash table: 작은 size이며, 데이터를 저장하는 서랍과 비슷, 각 서랍에는 번호가 매겨져 있다
- hash function: 큰 key space에 있는 값들을 어떤 규칙에 따라 table에 대응시킴(서랍에 넣는 과정)
- key space: 값들이 있는 곳

## collision

table에서 key 하나에 value 하나가 대응되면 O(1)인데, 여러 value가 대응되면 collision 발생

두가지 방안: chaining, open addressing

### Chaining

table 하나에 값들을 연결 리스트로 이어버림.

길어질수록 O(1)이 안됨!

그러면 hash function을 좋은 거 써야댐 

ex) division method(소수로 나눈 나머지), multiplication method(특정수 곱하기)

### Open Addressing

대응시키다 겹치면 빈 곳에 넣기

linear probing: 겹치면 바로 다음 빈 곳에 대응시킴, primary cluster 형성되면 O(n)돼버림

Quadratic probing: 겹치면 제곱수(1,4,9,16...)를 더해서 빈 곳을 찾아 대응시킴. secondary cluster 형성 가능

double hashing: 해쉬 함수를 한번더 적용

rehashing: table이 다 꽉찰 거 같으면 table을 새로 만듦

**완벽한 O(1)은 힘들다!**
