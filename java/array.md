# Array
예를 들어 성적을 모아놓은 배열 int[] score가 있음

## 배열 생성

처음 배열을 초기화하는 방법

- int[] score = {42, 35, 12, 100, 94}; → 자동으로 크기 설정, 값을 다 넣음
- int[] score = null
    
    score = new int[] {42, 35, 12, 100, 94}; → null로 초기화 했으면 배열 객체로 생성해야 함
    
- int[] score = new int[100] → 어떤 값을 넣을진 몰라도 크기가 100인 배열 생성

## 객체 참조 배열

다차원 배열이나 String[]은 배열 원소들이 각각 다른 객체의 주소를 담고 있음

힙 영역에서 객체가 다른 객체를 참조하는 것

## for문

```java
int[] scores = {42, 35, 12, 100, 94}; 

for( int score : scores) {
	sum += 1;
}
```

score는 scores를 인덱스 순서대로 다 돌면서 for문을 실행, 파이썬과 같음
