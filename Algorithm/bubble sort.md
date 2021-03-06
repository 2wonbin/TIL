# 버블 정렬(Bubble Sort)

## 정의 

서로 인접한 두 원소의 대소를 비교하고,   
조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘이다.

## 동작원리

1회전에 첫 번째 원소와 두 번째 원소를, 두 번째 원소와 세 번째 원소를, 세 번째 원소와 네 번째 원소를, …<br/> 이런 식으로 (마지막-1)번째 원소와 마지막 원소를 비교하여 이전 원소가 더 큰 경우 서로 교환한다.<br/>
1회전을 수행하고 나면 가장 큰 원소가 맨 뒤로 이동하므로 2회전에서는 맨 끝에 있는 원소는 정렬에서 제외되고, 2회전을 수행하고 나면 끝에서 두 번째 원소까지는 정렬에서 제외된다.<br/>
이렇게 정렬을 1회전 수행할 때마다 정렬에서 제외되는 데이터가 하나씩 늘어난다.<br/>

[[참조출처]](https://velog.io/@gillog/%EB%B2%84%EB%B8%94-%EC%A0%95%EB%A0%ACBubble-Sort)
