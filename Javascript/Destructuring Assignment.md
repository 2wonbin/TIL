# 구조 분해 할당 (비구조화 할당)
> 리액트 예제를 보다보면 많이 보이는 문법이다.    잘 익혀서 나중에 잘 쓸 수 있도록 하자.

## What is

**배열**이나 **객체**의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식 [[참조 : MDN]](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)   
➡말이 어렵지만 배열과 객체의 속성을 다룬다는 걸 알 수 있다.

## 배열 구조 분해 할당

``` javascript
const arr = [1,2,3,4,5];
const [a,b,c,d,e,f='가나다'] = arr;

console.log(`a=${a}, b=${b}, c=${c}, d=${d}, e=${e}`); // a=1, b=2, c=3, d=4, e=5
```
#### 순서에 맞게(자신의 인덱스에 맞춰) 참조/대입한다.
#### default값을 설정할 수 있다. 참조할 값이 없으면 설정해둔 default값으로 출력

### 값 변경
``` javascript
[x, y] = [y, x];
console.log(`x=${x}, y=${y}`);
```
#### 임의의 변수를 가져올 필요없이 변경할 수 있다.

### Rest(...)
➡ 키워드가 중요한게 아니다. '...'이 문법용어이다.
``` javascript
const names = ['홍길동', '신사임당', '이순신', '윤동주'];
const [ho, ...rest] = names;  
console.log(`ho=${ho}, rest=${rest}`);  // rest : '신사임당, '이순신', '윤동주'
```
### 함수의 리턴값
``` javascript
const foo = () => {
  return [3, 5, 7];
};

const [n1, n2] = foo();   //일부만 가져오는 것도 가능하다.
console.log(`n1=${n1}, n2=${n2}`); 
```
### 매개인자로 활용
``` javascript
const bar = ([x, y, ...rest]) => {  
  console.log(`x=${x}, y=${y}, rest=${rest}`);
};
  bar([9, 8, 7, 6, 5]); // ...rest : [7, 6, 5]
```
<hr />

## 객체 구조 분해 할당 ⭐⭐⭐

``` javascript
 const user = {
  id: 'honggd',
  name: '홍길동',
  hobby: ['축구', '농구'],
  age: 35,
  item: {
    car: '소나타',
    phone: {
      number: '01012341234',
    },
  },
};
```
### user 객체가 있고 내부 속성으로 hobby는 배열, item은 또 다시 객체, item 내부의 phone도 객체로 있는 모습이다.
``` javascript
const {
  id,
  name,
  profession = [],  
    item: {
      car,
      phone: { number },
    },
} = user;
```

####  ➡ 모습을 보아하니.. **key**값에 기존 property를 담고, 배열의 경우 타입만 지정, 객체 내부의 객체는 다시 그 값을 key값에 담는다.
#### key값은 사용자가 임의로 설정할 수 있다. ➡ 자리(위치)에 따라 참조를 하고 있다.

### 너의 이름은

``` javascript
const coffee = {
  name: '안티구아',
  place: '과테말라',
  taste: ['견과', '초콜렛'],
};

const {
  name: coffeeName,
  place,
  taste: [topTaste],
} = coffee;

console.log(`name=${coffeeName}, place=${place}, taste=${topTaste}`); // 구조 분해 파트에서 값의 이름을 재 정의할 수 있다.
```

### ...rest
``` javascript
const { name: variety, ...coffeeRest } = coffee;
console.log(`variety=${variety}`);
console.log(coffeeRest);
```

### 함수의 리턴값

``` javascript
const koo = () => ({
  position: {
    x: 234,
    y: 0.456,
  },
  radius: 3,
  color: 'black',
});

const {position: {x, y}, color, border = 1} = koo();  // border라는 값 새로 생성, 기본값을 1로 지정
```

### 매개인자에 사용
``` javascript
const handleUserWithId = ({id}) => {  //인자로 오는 객체의 'id'값을 함수에 전달 
  console.log(id);
}
handleUserWithId(user); //'홍길동'


const handleUserWithHobby = ({ hobby: hobbies }) => {   //입력받는 객체의 key값 'hobby'를 함수 안에서 hobbies로 사용하겠다.
//   hobby.forEach((element) => {
//     console.log(element);
//   });
hobbies.forEach((hobby, index, hobbies) =>
 console.log(hobby, index, hobbies)
  );
};

handleUserWithHobby(user);
```
### 심화예제
``` javascript
 const input = document.querySelector('#query');
input.addEventListener('keyup', ({ target: { value } }) => {    // e.target.value 역시 자바스크립트 object < '.' 연산자로 내부 함수에의해 접근 가능
  console.log(value);
});

```