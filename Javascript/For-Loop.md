# for 키워드를 사용하는 자바스크립트 반복문

## 기존 for를 위한 반복문
``` javascript
const arr = [];
for(let i= 0; arr.length < 10; i++){
  arr.push[i+1];  // [1,2,3,4,5,6,7,8,9,10]
}
```

## for..in
```javascript
for(변수 in 객체)
/*객체 자리에 배열이 올 경우 배열요소(size,contains....)들도 같이 출력된다.*/
/* 변수 자리엔 객체 내부 키값이 들어온다, 배열의 경우 인덱스*/
/* 객체의 value값이 필요하다면 객체[변수]로 찾아야한다.*/

for(let i in obj){
  console.log(i, obj[i])
}
```

## for..of
``` javascript
for(변수 of 배열)
/*ES6, Iterator속성을 가진 컬렉션 요소들의 반복에 사용*/
/* 말이 좀 어렵지만 대부분 배열의 순차적 요소 접근에 이용된다고 생각하겠다.*/
/* in은 객체 접근 시 , of는 배열 접근 시 라고 생각해도 크게 오류가 없어 보인다.*/
```


## forEach를 사용한 반복문
``` javascript
const arr =[];
arr.forEach(요소,인덱스?,배열? => {실행문} )
/* 마찬가지로 배열 첫 요소부터 반복실행*/
```