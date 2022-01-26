## Intro

데이터: 실험, 시뮬레이션 등 과학적, 경험적으로 얻어진 사실(조각)들

정보: 데이터가 조직되면 정보지만 데이터랑 혼용해서 씀

데이터구조: 컴퓨터가 데이터를 저장하고 조작할 수 있는 방법

**C언어 기준으로 설명**

# Algorithm
알고리즘: 문제를 해결하기 위한 잘 정의된 지시(=microoperation)들의 유한한 리스트
initial state와 end state가 있어야 한다

## 알고리즘 평가
- 옳은가 → 수학
- 명확한가 → 프로그래밍 언어로 표현하면 됨
- 효율적인가 → complexity theory로 결정

## 알고리즘 개발 절차
1. 솔루션 일단 만듦(informal solution)
2. 수학적으로 검증(induction, counter example, contradiction)
3. 프로그래밍 언어로 구현
4. machine independent 한가, complexity는 좋은가 평가

Fetch-Execute Cycle

1. Fetch the next instruction
2. Decode the instruction
3. Execute the instruction

2랑 3은 CPU에서 하는 것

Machine Instructions set

- Data transfer: LOAD, STORE
- Arithmetic/Logic: 연산, and or xor, shift rotate
- Control: 프로그램 실행, 점프(현재꺼 다 끝내지 않고 다른 거 실행!)

이렇게 하여 함수 안에서 함수 호출과 재귀함수가 가능한 것이다

재귀함수 규칙

- base case(termination condition) 반드시 존재
- 점진적으로 문제를 해결해나가야 함
- 서브 함수들이 똑같은 작업을 하면 안됨
- divide conquer

동적할당과 jump(시스템 내장 스택 사용) 등등 때문에 반복문보다 미세하게 느림

그러나 재귀함수가 코드짤 때 효율적임

언제쓰냐?

- 반복문으로 짜기 어려울 때
- 재귀하면서 서브문제들을 반복적으로 해결하지 않을 때

이진탐색(Binary Search): 정렬된 숫자 리스트에서 반씩 쪼개면서 숫자 찾음, O(logn)

n/2번째(딱 중간)부터 타겟이랑 비교해서 타겟이 더 크면 오른쪽, 작으면 왼쪽으로 가서 다시 반씩...

maximum subsequence sum problem: 정렬 안된 숫자 리스트에서 합해서 가장 큰 수가 되는 서브리스트를 찾는 문제

1. 모든 sum을 다 만들어서 비교, loop 3개 → O(n^3)
2. 1과 같지만 loop 2개 → O(n^2)
3. 반씩 쪼개서 max(왼쪽에서 가장 큰거, 오른쪽에서 가장 큰거, 왼쪽 끝에서 시작하는 거 중에 가장 큰거, 오른쪽 첫번째에서 시작하는 거 중에 가장 큰거) → 재귀함수로 O(nlogn)
