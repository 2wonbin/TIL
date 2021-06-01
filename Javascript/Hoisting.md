# 호이스팅
[[참조출처 : [javascript 호이스팅(hoisting)이란?]]](https://ojava.tistory.com/144)

``` javascript
catName("chloe");

function catName(name){
  console.log("My cat's name is" + name);
}
```

함수의 선언코드가 함수의 정의보다 먼저 작성됐더라도 자바스크립트 환경에선 정상적으로 실행된다.

## 정의
지바스크립트에서 코드에 선언된 변수 및 함수를 코드 최상단으로 끌어올려진다.   
함수 내에서 선언한 함수 범위의 변수는 **해당 함수의 최상위로**   
함수 박에서 선언한 전역 범위의 전역변수는 **스크립트 단위의 최상위**로 끌어올려진다.

## 주의사항
``` javascript
noDefine();

function noDefine(){
  console.log("not define : " + name); // undefined
  var name = "kim";

  console.log("define : " + name);  //kim
}
```
의 결과는 다음과 같다.

``` javascript
noDefine();

function noDefine(){
  var name; // var로 호출한 변수를 호이스팅
  console.log("not define : " + name); // undefined
  name ="kim";
  console.log("define : " + name);  //kim
}
```
하지만 var 선언 없이 진행한다면
### 함수 내에서 변수 선언 명령어를 제외하고 선언 시 전역변수의 형태로 사용된다.

``` javascript
noDefine();

function noDefine(){
  console.log("not define : " + name); // kim
  name ="kim";
  console.log("define : " + name);  //kim
}
```
## 함수 호이스팅
함수 호이스팅은 함수 선언식인 경우에만 적용된다.

### const, let
es6에 등장한 const, let 키워드는 호이스팅이 적용되지 않는다.