# append()와 appendChild() 차이

## 공통점
두 함수 모두 정해둔 부모 요소 뒤에 자식 요소를 추가한다.

## append()
1. 노드 객체 / DOM String(text)를 사용할 수 있다
``` javascript
//노드 객체
const parent = document.createElement('div');
const child = document.createElement('p');

parent.append(child);   //<div><p></p></div>
//DOM String

const parent = document.createElement('div');
parent.append('얍');  //<div>얍</div>

```
2. 여러 요소를 받을 수 있다.
``` javascript
const div = document.createElement('div');
const p = document.createElement('p')

document.body.append(div,p, 'hello');   //<body><div></div><p><p>hello</body>
```
3. 리턴값이 존재하지 않는다.
``` javascript
console.log(document.body.append(div,p, 'hello')) //undefined
```

## appendChild()

1.하나의 node 객체만 받을 수 있다 == 여러 요소 받을 수 없다 + text(DOM String)을 받을 수 없다.
``` javascript
const parent = document.createElement('div');
const child = document.createElement('p');

const parent = document.createElement('div');
parent.append('얍');  //Uncaught TypeError
```

2. 리턴값을 반환한다 (Node 객체)
``` javascript
const div = document.createElement('div');
console.log(document.body.append(div)); //div(Node Object)

```