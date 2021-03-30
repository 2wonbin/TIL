# Truthy & Falsy (참과 거짓)
데이터 타입이 boolean이 아니어도 그 자체로 true와 false의 속성을 가지는 경우가 있다.<br/>
## True
비교 연산 시 같은 값, 심지어 값이 존재하는 것만으로 true의 값을 갖는다.<br/>
(falsy하지만않으면 모든 값은 true가 된다..)<br/>
[출처 : MDN](https://developer.mozilla.org/ko/docs/Glossary/Truthy)<br/>
* 주의사항
  * [], {}, new Date() : 빈 배열, 빈 객체 역시 존재 자체로 true의 값을 가진다.
  * "false" : 문자열로 존재할 경우엔 true 값을 갖는다.
```javascript
if([]) console.log("야호"); // 야호
if("false") console.log(야호);  //야호
```
## Falsy
*false*, *undefine*, *null*, *NaN*, '', *0* 의 경우 false의 속성을 가지고 있다.
``` javascript
if(0){
  console.log("Truthy!")
  } else {
  console.log("falsy!") -> 출력값.
  }
  
