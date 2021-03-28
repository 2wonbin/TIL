# DIP(Dependency Inversion Principle ; 의존성 역전의 원칙)
> 이 게시글엔 김영한님의 <스프링 핵심 원리 - 기본편>  강의 내용 일부가 포함되어 있습니다.<br />
> 문제가 될 경우 삭제합니다. 


**추상화**에 의존해야 한다. 구체화에 의존해서는 안된다<br />
== 구현 클래스의 의존하지 말라. **인터페이스**에 의존하라.<br />
== **역할**에 의존해야한다.

[**의존성**]은 무엇일까?<br />
해당 주체(클래스 or 함수 등)이 누군가 필요로 함<br />
[출처](https://medium.com/@homekeeper89/%EC%9D%98%EC%A1%B4%EC%84%B1%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-e3276e704157 "")<br />

## 잘 짜여진 설계
```java 
public Order createOrder(Long memberId, String itemName, int itemPrice) {
        Member member = memberRepository.findById(memberId);
        int discountPrice = discountPolicy.discount(member, itemPrice);

        return new Order(memberId, itemName, itemPrice, discountPrice);
    }
   ```
   Order의 입장에선 자신은 discount 대한 결과는 알지도, 관여할 수 도 없다.<br />
   discount는 DiscountPolicy에서 모두 처리한다<br />
   Order는 오로지 리턴된 결과를 받아서 처리할 뿐.<br />

```java
public class OrderServiceImpl implements OrderService{

 private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
 private final DiscountPolicy discountPolicy =new RateDiscountPolicy();
 
 .....
 .....
 ```
## DIP를 위반하는 경우
OrderServiceImpl이 DiscountPolicy를 의존해야하지만 (추상; interface에 의존)<br />
현실은 DiscountPolicy도 의존하면서 (FixDiscountPolicy) RateDiscountPolicy를 의존하고 있다 (== 추상에 의존하면서 구체에도 의존)<br />
=> DIP 위반
=> DIP 위반의 결과. DiscountPolicy의 변경사항이 ordeServiceImpl의 코드를 바꾸는 결과를 도출.
