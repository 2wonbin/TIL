# 화살표 함수(Arrow Function)
ES6문법. 함수표현식, 익명함수를 대체한다.<br/>
앞으로 많이, 자주 등장할 표현이다. 나올 때 마다 정리한다.

 1. function 키워드를 생략한다.
 ``` javascript
 const print = name => {  //매개 변수부가 하나일 경우, 괄호 생략 가능
   console.log(`${name}님 반갑습니다.`)
 };
 ```

 2. 몸통부 코드가 한 줄인 경우, { return(키워드) } 모두 생략 가능
 ``` javascript
 const multiply = x => x**;
 ```

 - 주의사항
 1. 화살표함수의 'this'는 parent scope의 this를 가져다쓴다. 보통 parent scope가 존재하지 않아 window 객체를 가리킨다.