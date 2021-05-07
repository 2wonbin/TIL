# Spread & Rest
> 공통적으로 객체와 배열에서 사용된다.   
> '...' 키워드가 핵심이다. spread와 rest는 의미별 별칭?을 나타낼 뿐이다.

## Spread

### 배열의 경우
기존배열을 합치기 위해선 push, concat, splice와 같은 함수를 사용했어야 했다. spread는 배열의 합을 굉장히 간단한 문법으로 해결하게 한다.

``` javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = [a,... arr1, b, c];  // [1, a, b, c, 2, 3, 4, 5]
```

### 객체의 경우
기존 객체에 영향을 주지 않고(그대로 가져와서) 새로운 객체를 생성
``` javascript
const info ={
  name: 홍길동,
  age: 30
}

const moreInfo ={
  ... info,
  height: 170
}
```

## Rest
말 그대로 '나머지'라고 생각하는게 정신건강에 이롭다.
구조 분해 할당(비구조화 할당)과 굉장히 잘 어울러져 보인다.

### 배열의 경우
``` javascript
const arr = [1, 2, 3, 4, 5, 6];
const [a, b, ... rest] = arr;
console.log(a, b);  // 1, 2
console.log(rest);// [3, 4, 5, 6]
```

### 객체의 경우

``` javascript
const {name, ...rest} = moreInfo;
console.log(rest) // {age: 30, height: 170}

```

### parameter & argument

함수의 파라미터가 몇개가 올 지 명확한 상황이 아닐 경우 rest 파라미터 사용
배열의 모든 요소를 인자로 넣고 싶을때 spread 사용

<hr />

[[참조링크 : 07. spread 와 rest 문법 ]](https://learnjs.vlpt.us/useful/07-spread-and-rest.html)   
[[참조링크 : 자바스크립트 Spread와 Rest 문법 차이점]](https://medium.com/@shlee1353/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-spread%EC%99%80-rest-%EB%AC%B8%EB%B2%95%EC%A0%95%EB%A6%AC-f42efa73d3db)   
[[구조분해할당 정리]](https://github.com/2wonbin/TIL/blob/main/Javascript/Destructuring%20Assignment.md)
