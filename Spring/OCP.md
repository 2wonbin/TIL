# OCP , 개방 - 폐쇄 원칙 (Open / Closed Principle)
> 작성한 코드는 김영한님의 강의 [<스프링 핵심 원리 - 기본편>](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8/dashboard) 의 내용에서 일부 발췌하였습니다.   

## 소프트웨어 요소는 개방에는 열려있으나 확장에는 닫혀있어야한다.

❓❓ 이게 무슨 말이지 ❓❓

### Back to the Polymophism
자동차(interface, 역할) - 🚗, 🚓, 🚌, 🚚 (implements, 구현체).   
공연의 배역(역할) - 배우(구현체)
어떤 구현의 모습이 다를 뿐 역할은 같다.
**인터페이스를 구현한 새로운 클래스를 만들어 새로운 기능을 구현**

### 다형성을 적용

``` java
public class MemberService {
  private MemberRepository memberRepository = new memberRepository();
}

public class MemberService {
  // private MemberRepository memberRepository = new memberRepository();  --> 코드 변경 발생. 확장에 닫혀있지 않음.
  private MemberRepository memberRepository = new JdbcMemberRepository();
}
```
🚨 다형성을 적용했지만 OCP 원칙을 지킬 수 없다.
 
## 구성영역과 사용영역을 분리

``` java

public class AppConfig{
  public MemberService memberService(){
    return new MemberServiceImpl(memberRepository());
  }
}
```

### 구성 영역의 변경으로 '사용 영역'의 코드 변경없이 원하는 결과를 이뤄낼 수 있다.
### 구성 영역(구현 객체를 생성 + 연결) = 공연 기획자, 공연의 기획자는 공영 참여자(구현 객체)를 모두 알아야한다.