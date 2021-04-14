# @Bean 과 @Component의 차이
> 작성한 코드는 김영한님의 강의 <스프링 핵심 원리 - 기본편> 의 내용에서 일부 발췌하였습니다. 문제가 될 경우 삭제합니다.


두 어노테이션 모두 스프링 빈을 관리하는 방법 다루는 방법이다. <br/><br/>
**@Bean**의 경우 메소드를 통해 반환되는 객체를 Bean으로 등록하고 <br/>
```java
//AppConfig.java

@Bean
public MemberService memberService(){ 
  return new MemberRepository(memberRepository());
}
```

**@Component**의 경우 타입(클래스)를 Bean으로 등록하는 방식이다. <br/>
``` java
@Component  // 구현체를 Component로 변환
public class MemberServiceImpl implemnets MemberService{
  ....
}
```

메소드에 @Component를 선언할 경우 컴파일 오류가 난다. 반대도 마찬가지다.<br/>
[참조링크](https://kimeck.tistory.com/10)<br/>

*기록일 : 21.04.14*
