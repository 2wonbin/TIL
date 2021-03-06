# 2차 정리(21.05.05)

[[참조출처 : [10분 테코톡] 🌱 시드의 제네릭]](https://www.youtube.com/watch?v=Vv0PGUxOzq0)

## 제네릭이란
클래스 / 메소드에서 사용할 내부 데이터 타입을 **외부**에서 지정하는 것.

## 제네릭 클래스
클래스 선언에 **타입 매개변수**가 쓰일 때, 제네릭 클래스라고 한다.
``` java
class FruitBox<T>{....}

class FruitBox<Apple>{    
    //외부의 타입이 내부 타입 매개변수로 대입, 실제로 변경되는 것은 아님 --> Type Eraser 참조

    List<Apple> fruits = new ArrayList<>();

    public void add(Apple fruit){
        fruits.add(fruit);
    }
}

FruitBox<Apple> appleBox = new FruitBox<>();    //외부에서 Apple타입의 인스턴스 생성
```

## 제네릭 사용 이유

타입 체크를 강력하게 하여 런타임에서 발견될 에러를 **컴파일** 단계에서 검증하기 위함.
--> 컴파일시 타입체크가 되기 때문
--> 형변환을 따로 해줄 이유가 없다.

## 제네릭 메소드

``` java
public <T> void add(T t){
    ....
    //타입 T의 유효범위는 블록 내부까지만
}
```
### 제네릭 클래스와 제네릭 메소드의 중첩
둘의 타입 매개 변수가 같다면(T) 제네릭 메소드의 타입 매개변수가 우선
``` java
class Name<T>{
    public <T> void printClassName(T t){
        System.out.println(t.getClass().getName());
    }
}

public static void main(Stiring[] args){
    Name<String> name = new Name<>();
    Class.printClassName(1);        //java.lang.Integer
    Class.printClassName(3.14)      //java.lang.Double
}
```
## 타입매개변수의 제한 (21.05.10)

### t extends T

't' 클래스는 T 자신이거나 T의 하위 클래스여야 한다(== 자식/후손 클래스)



~~t super T~~   
~~'t' 클래스는 T 자신이거나 T의 상위 클래스여야한다(== 부모 / 조상 클래스)~~

### 비경계 와일드카드 <?>
어떤 타입이든 오는 것이 가능하다
``` java
- List<?> <- List<A>는 가능하지만, List<Object> <- List<A>는 컴파일 오류

- List<?>의 요소의 타입은 Object이다.

- List<?>에는 null만 삽입할 수 있다. == List 내부 요소간 타입이 유지되지 않는 문제가 발생하는 걸 막기위해서.
```

### 와일드카드의 상한
``` java
? extends T의 형태 == T 자신이거나 T의 하위 클래스의 어느 타입이든 요소로 올 수 있다.
- List<? extends T> 에서 Get 한 원소는 T 혹은 T의 하위 클래스 == 다형성에 따라 T로 읽을 수 있다.

- 마찬가지로 List<? extends T> 에는 null 값만 대입할 수 있다 == List 내부 요소간 타입이 유지되는 문제가 발생한다.
```

### 와일드카드의 하한
``` java
- ? super T === 자신이거나 T의 상위 클래스 중  어느 타입이든 요소로 올 수 있다.
- 어떤 타입이 이든 읽을 수 있도록 Get 한 요소는 Object
- List<? super T>에는 T 자신이거나 T의 하위 클래스만 삽입 가능

```
<hr/>



# 제네릭(Generics)
다양한 타입의 객체를 다루는 메소드나 컬렉션 클래스에 컴파일 시 타입체크를 해주는 기능이다 <br/>
--> 컴파일 시에 체크하기 때문에 객체의 '타입 안정성'을 높이고 형 변환의 번거로움 제거.<br/>

## 제네릭 클래스 선언

```java
public class Champion<T> {

    T passive;

    public T getPassive() {
        return passive;
    }

    public void setPassive(T passive) {
        this.passive = passive;
    }
}
```
여기서 T를 **타입 변수** 라고 한다. (T는 타입을 의미하는 임의의 참조형 타입이다. == 어떤 단어가 와도 상관없다. 수학의 x처럼) <br/>

```java
Champion<String> champion = new Champion<>();
// 다른 클래스에서 champion의 제네릭 타입변수 자리에 String을 선언.

....

public class Champion {

    String passive; // T의 자리에 모두 String을 지정한 것과 같다.

    public String getPassive() {
        return passive;
    }

    public void setPassive(String passive) {
        this.passive = passive;
    }
}
```
## 제네릭 클래스 객체 생성 및 사용
```java
Box<Apple> appleBox = new Box<Apple>();
```
참조변수와 생성자에 대입한 타입이 일치해야한다.
```java
Box<Apple> appleBox = new Box<Grape>(); ///컴파일 오류
```

## 상속의 경우
일반 클래스의 경우 상속후 제네릭 클래스를 선언한다면 컴파일 오류다.
```java
public class Apple extends Fruit{...}

....

Box<Fruit> appleBox = new Box<Apple>(); //컴파일 오류
```

제네릭 클래스 **타입이 상속관계**에 있고 타입이 다른건 오류를 만들지 않는는다.
``` java
public class FruitBox<T> extends Box{...}
...
Box<Apple> appleBox = new FruitBox<Apple>();    // 다형성
```

[출처](https://www.notion.so/4735e9a564e64bceb26a1e5d1c261a3d)


