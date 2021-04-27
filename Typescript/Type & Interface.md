# 타입과 인터페이스

### 객체에 대해서 둘 다 활용법이 다르지 않다.
``` typescript
interface person{
  name: string;
  age: number;
}

type person{
  name: string;
  age: number
}
```

## 차이점
### 타입은 한 번 선언된 이상 확장이 불가능 
 ``` typescript
  type person{
    name: string
  }

  type person{  //'person' 식별자가 중복되었습니다.ts(2300)
    age: number;
  }
 ```
### 인터페이스는 확장이 가능하다.
 ``` typescript
  interface person{
    name: string
  }

  interface person{ 
    age: number;
  }

  var one: person ={
    name: '원',
    age: 20
  }
 ```

 ### 인터페이스는 객체에 대해서만 사용 가능하다.
  ``` typescript
  interface person{
    name: string
    age: number
  }

  type person{  
    name: string;
    age: number;
  }

  type person = string | number;

  interface person = string | number; // OO은 형식만 참조하지만, 여기서는 값으로 사용되고 있습니다.ts(2693)
 ```

 ### 정리
 객체 타입을 지정할 땐 **interface**를 사용하고, 그 외엔 **type**을 사용하여 타입을 규정한다.

 [참조 : 타입스크립트 type과 interface의 공통점과 차이점](https://yceffort.kr/2021/03/typescript-interface-vs-type)
 [참조 : 타입과 인터페이스의 차이점은 무엇인가요?](https://www.inflearn.com/questions/108559)