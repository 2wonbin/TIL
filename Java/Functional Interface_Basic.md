# 자바 함수형 인터페이스 기본

[[참조출처: '망나니 개발자'님 - 람다식과 함수형 인터페이스]](https://mangkyu.tistory.com/113)

## 자바 기본 제공 함수형 interface

### Supplier
매개변수없이 반환값만 갖고 있는 함수형 인터페이스

``` java
@FunctionalInterface
public interface Supplier<T>{
  T get();  //추상메소드 get을 가지고 있다.
}

Supplier<String> supplier = () -> "Hello World!"
System.out.println(supplier.get()); //"Hello World!"
```

### Consumer<T>
객체 T를 매개변수로 받으면서 반환값은 없는 함수형 인터페이스
```java
@FunctionalInterface
public interface Consumer<T>{

  void accept(T t); // 객체 T를 받지만 반환값은 없는 추상메소드 accept
}

```


### Function<T,R>
객체 T를 매개변수로 받아 처리 후 R로 반환하는 함수형 인터페이스
``` java

@FunctionalInterface
public interface Function<T, R>{
  R apply(T t)  // T를 변수로 받아 R로 리턴하는 추상메소드 apply
}

Function <String, Integer> function = str -> str.length;
function.apply("Hello World");  //11
```

### Predicate<T>{

객체 T를 매개변수로 받은 후 결과값으로 Boolean 리턴
``` java
@FunctionalInterface
public interface Predicate<T> {
  boolean test(T t) // T를 매개변수로 받아 Boolean을 리턴하는 추상메소드 test
}

Predict<String> predicate = str -> str.equals("Hello World");
predicate.test("Hellow World"); //true
```

