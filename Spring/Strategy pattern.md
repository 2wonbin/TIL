# 전략패턴 (Strategy Pattern)
>전략 패턴은 실행 중에 알고리즘을 선택할 수 있게 하는 행위 소프트웨어 디자인 패턴이다.
## 전략패턴의 필요
특정 기능이 추가 시 유연하게 확장할 수 있는 설계 구현

## 전략 패턴 설계
### 전략 생성
``` java
public interface DiscountPolicy {

    /**
     * @return 할인대상금액
     */

    int discount(Member member, int price);
}
```
### 전략 클래스들은 DiscountPolicy 인터페이스를 상속하고 discount 메소드를 오버라이딩 한다.
``` java
public class FixDiscountPolicy implements DiscountPolicy{

    private int discountFixAmount = 1000;

    @Override
    public int discount(Member member, int price) {
        if(member.getGrade() == Grade.VIP){
            return discountFixAmount;
        } else{
        return 0;
        }
    }
}
```
``` java
public class RateDiscountPolicy implements DiscountPolicy{

    private int discountPercent = 10;

    @Override
    public int discount(Member member, int price) {
        if(member.getGrade() == Grade.VIP){
            return price * discountPercent / 100;
        } else {
            return  0;
        }
    } 
}
```
### 전략 주입 및 유지 보수
```java
    @Bean
    public OrderService orderService(){

        return new OrderServiceImpl(memberRepository(), discountPolicy());  // 할인 정책 주입
    }

    @Bean
    public DiscountPolicy discountPolicy(){
       //return new FixDiscountPolicy();
        return new RateDiscountPolicy();    //할인 정책 변경
      // return new OOOODiscountPolicy();   // 새로운 할인 정책 필요시 새로운 전략을 추가해서 주입하기만 하면 된다.
    }
}
```
### 구현체에서 할인 정책을 주입받아 주입받은 전략 수행
``` java
public class OrderServiceImpl implements OrderService{

  .....
  
    public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = discountPolicy;
    }
  .....
  
```
