# DI(Dependency Injection ; 의존관계 주입)

> 이 게시글엔 김영한님의 <스프링 핵심 원리 - 기본편>  강의 내용 일부가 포함되어 있습니다.<br />
> 문제가 될 경우 삭제합니다. 


## 의존관계란
- 정적인 의존관계 : 실제 코드의 흐름(다이어그램, import 대상 등..) 을 보고 의존관계가 파악이 가능 => 실행하지 않아도 흐름 분석이 가능.
- 동적인 의존관계 : 런타임 중에 흐름이 파악. 


## 의존관계 주입
런타임(실행)중에 외부에서 객체를 구현하고 그것을 서버에 전달. 서버와 클라이언트 간 의존관계가 연결되는 것을 **의존관계 주입** 이라고 한다.
```java
//AppConfig.java  // 외부에서 객체 간 의존관계를 제어, 
                  //구현로직에 따라 정적인 의존관계 변경없이(구현되는 내부 클래스들의 코드를 건들지 않고) 제어한다.

    public OrderService orderService(){

        return new OrderServiceImpl(memberRepository(), discountPolicy());
    }

    public DiscountPolicy discountPolicy(){
       //return new FixDiscountPolicy();
        return new RateDiscountPolicy();    
    }
```
### 효과
1. 클라이언트의 구성을 변경하지 않고도 호출되는 대상의 인스턴스(객체)를 제어할 수 있다
2. 정적인 의존관계에 변경없이 동적인 의존관계를 쉽게 변경이 가능 == 변경사항 발생시 코드를 변경하지 않아도 된다
