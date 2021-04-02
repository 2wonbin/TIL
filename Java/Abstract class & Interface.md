# 추상클래스와 인터페이스

## 추상클래스와 인터페이스의 차이 
- 추상클래스를 상속한 클래스는 반드시 내부 추상메소드를 구현하여야 한다.<br />
그에 반해 인터페이스는 속성을 제공만 할 뿐 구현 의무는 없다.

- 추상 클래스는 단 하나의 클래스를 상속하지만 <br />
인터페이스는 다중 implements가 가능하다

## 인터페이스만의 특징
- 자바 8 버전부터 default 예약어를 통한 일반 메소드 구현이 가능하다
``` java
public interface Sized {
  int size();
  default boolean isEmpty() {}
    return size() == 0;
  }
//isEmpty() 메서드가 바로 default 메서드이다. 
//위 Sized 인터페이스를 구현하는 모든 클래스들은 isEmpty의 구현도 상속받게 된다. 
//이렇게 인터페이스에 디폴트 메서드를 추가하면 소스 호환성이 유지
}
```
[출처](https://devfunny.tistory.com/350)
- 인터페이스의 필드는 (public) static final로 선언된다
why?<br />
1. 인터페이스의 변수는 스스로 초기화 될 권한이 없다.
2. 인터페이스 생성 시점엔 어떤 인스턴스도 존재하지 않기 때문

[출처](https://donggyu9410.medium.com/%EC%B6%94%EC%83%81%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4-b238d1ad04e5)

