# 메소드 참조(Method Reference)
기존 메소드를 람다식으로 사용이 가능하다.

``` java
//기존
Consumer<String> print = string -> System.out.println(string);
print.accept("안녕");

//메소드 참조 : parameter를 그대로 메소드 호출 시 사용할 땐 생략이 가능하다. 
//== accept 메소드 실행 시 전달되는 인자와 System.out.println 호출 시 전달되는 인자가 같으면 생략이 가능
Consumer<String> print = System.out::println;

```
[[참조출처:메소드 참조]](https://velog.io/@new_wisdom/Java-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%B0%B8%EC%A1%B0)

### 자바 내장 메소드도 참조가 가능하다.
``` java
// String 클래스가 제공하는 메소드 length() 참조 (문자열의 길이 리턴)
Function<String, Integer> strLength = String::length;
System.out.println(strLength.test("안녕하세요")); // 5
```

### 클래스 내부 메소드 참조 와 생성자 참조

``` java
Function<String, Person> PersonName = Person::new;
// 생성자 메소드 내부 파라미터의 타입으로 객체 생성 (해당 초기화 함수가 있어야한다.)

Bipredict<Person, Person> samePerson = Person::equals;
System.out.println(samePerson.test("홍길동", "홍길동"))   //equals, hashcode 메소드 override 시에만 동일한 객체로 간주.
```