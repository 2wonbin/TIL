# 단축 평가

*논리곱(&&)* 연산자와 *논리합(||)* 연산자는 논리 연산의 결과를 결정하는 피연산자의 타입을 변환하지 않고 그대로 반환한다.   
이를 **단축평가**라 한다. 단축평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하느 것을 말한다.


|표현식|결과|
|---|---|
|true II anything | true |
|false II anything | anything |
|true && anything | anything |
|false && anything | false |
(md 테이블 형식과 겹쳐 |를 영문자 I로 대체)

## IF 대체

어떤 조건이 Truthy한 값일 떄 무언가를 한다면 논리곱(&&) 연산자로 대체할 수 있다.
``` javascript

const done = true;
let message = '';

//if를 사용
if(done) message = '완료';

//단축 평가 사용
message = done && '완료'  // done = true. 우항 실행 X

```

조건이 Falsy값일때 무언가를 한다면 논리합(||) 연산자 표현식으로 if를 대체할 수 있다.
``` javascript
const done false;
let message = '';

//if를 사용
if(!done) message = '완료';

//단축 평가 사용
message = done || '미완료';   // 미완료 리턴

```
[출처 : [ 이웅모, 모던 자바스크립트 Deep Dive ], p.119 - p. 120] 