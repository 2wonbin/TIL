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

