# 데이터 중복 줄이기 1

> 한 상품에 이미지 파일이 존재한다면 이미지 파일 만큼 row가 생긴다.   
> 그 중 대표 이미지 하나만 선택하고 싶을 때 어떻게 해야할 지 고민해보았다.   
> 물론 많은 해결 방법이 있겠지만 시도한 방법을 정리해본다.

## join을 통한 분류

|상품|이미지|....|
|---|----|----|
|사과|1.jpg|....|
|사과|2.jpg|....|
|바나나|1.jpg|....|
|바나나|2.jpg|....|

1.jpg만 뽑고싶다.<br/>

**group by** 를 이용하여 이미지의 min value를 구하였다 (기준이 변경된다면 그때마다 새롭게 묶어서 처리해야한다.)

|상품|이미지|
|---|----|
|사과|1.jpg|
|바나나|1.jpg|

그 후 다시 원래 Table과 join하여 공통된 부분만 남기도록 하였다

## 문제점
1. join이 많아질수록 성능의 문제가 발생할 수 있다.
2. join이 많아질수록 한 눈에 들어오지 않는다.