# 람다식(Lambda Exepression)

*자바스크립트 화살표 함수와 닮아있었고, 코드가 조금 더 간결해지는 효과가 있어 공부해보았다.*

[출처](https://www.youtube.com/watch?v=3wnmgM4qK30&list=PLW2UjW795-f6xWA2_MUhEVgPauhGl3xIp&index=157)

## 함수와 메소드의 차이

- 함수는 일반적 용어, 메소드는 객체 지향 개념 용어

- 함수는 클래스에 독립적, 메소드는 클래스 종속적

## 람다식이란

함수를 간단한 식으로 표현하는 방법

``` java
int max(int a, int b){
  return a > b? a : b;
}

>>>
// 함수(메소드) 이름과 반환타입 제거하고 블록 앞에 '->' 를 추가
(int a, int b) ->{ return a > b > a : b; }

>>>
//반환 값이 있는 경우 식과 값만 적고 'return'문 생략 가능, 끝에 ';' 붙이지 않는다.
//매개 변수 타입이 추론 가능하면 생략이 가능 (대부분 case)
(a, b) -> a > b ? a : b

```

### ※주의사항※

``` java
//1. parameter 하나인 경우, 타입이 없을 때만 괄호 생략 가능
(a) -> a * a // O
a -> a * a // O
int a -> a * a // error, (int a)로 전달해야한다.

//2. 블록 안의 문장이 하나일때, 괄호{} 내용 생략 가능(';' 생략)
(int i) -> System.out.println(i)

//3. parameter가 없을 경우
int roll(){
  return (int)(Math.random() * 6);
}

>>

 () -> (int)(Math.random() * 6);
 // 함수명, 반환타입 제거. return 키워드, {} 제거. 형변환을 위해 선언한 키워드는 생략할 수 없다.
```

## 익명객체

- 람다식은 익명 함수가 아니라 익명 객체이다

``` java
(a, b) -> a > b ? a : b

==

new Object() {
  int max(int a, int b){
    return a > b ? a : b ;
  }
} // 익명 객체 : 객체의 선원과 생성을 동시에 처리. cf) 익명 클래스

//※ 객체를 다루려면 참조 변수가 필요, 참조변수의 타입은?
Object obj = (a, b) -> a >b ?  a : b;
int value = obj.max(3,5)  // 컴파일 에러, Object 클래스에는 max()가 없다. >> 함수형 인터페이스로 해결
```
