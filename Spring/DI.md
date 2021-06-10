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

<hr />

> 도저히 무슨 소리인지 감이 안와서 보충합니다. (21.04.15)

여태 공부해온 방식으로는 RemoteControl 클래스의 자원을 사용하기 위해선 따로 객체를 생성해서 이용하였다
``` java
// SamsungTv.java
....
private RemoteControl rc = new RemoteControl();
....
```

## DI를 하는 이유
 1. 스프링 컨테이너 내부에서 Bean들을 관리하기때문에 원하는 객체를 주입받아 사용하기 편리
 2. 객체를 내부에서 생성할 시 객체 변경시 처리해야할 작업이 늘어난다. (여기까진 그렇게 와닿지 않는다)
 3. **객체를 내부가 아닌 외부 환경설정 변경만으로도 유연하게 변경하기 위해. -> 구현하는 클래스에는 아무 영향을 주지 않는다.** 
 4. (다 필요없고 그냥) 생산성과 유지보수를 위해

``` java
public class SamsungTv implements Tv {
....
@Autowired
public SamsungTv(RemoteControl remocon) {
  System.out.println("SamsungTv(RemoteControl) 객체 생성");
  this.remocon = remocon;
  }
}
```
<hr/>

## 의존성 주입 방식 (21-06-10)
[[참조출처 : Spring DI의 모든 방법 @Autowired / 생성자 주입 ]](https://leejisoo860911.tistory.com/2)

### 필드 주입
생성된 클래스에 필드로 선언한 뒤 @Autowired 어노테이션을 붙여준다.

``` java
public class MemberService{

  @Autowired
  @Qualifier("userDao")   //Bean 이름 지정 가능
  private MemberDao memberDao;
}

```
### setter를 통한 주입( 꼭 setter일 이유는 없음, 동일한 역할만 한다면 어떤 이름이 와도 상관없다. == method injection)

``` java
public class MemberService{

  private MemberDao memberDao;

  @Autowired
  public setMemberDao(MemberDao memberDao){
    this.memberDao = memberDao;
  }
}

```
### 생성자 주입
가장 권장되는 방식, spring 4.3 버전 이후에 필드가 하나 존재한다면 @Autowired 어노테이션이 없어도 Bean으로 등록된다.
``` java
public class MemberService{

  private MemberDao memberDao;

  // @Autowired
  public MemberService(MemberDao memberDao){
    this.memberDao = memberDao;
  }
}
```
## Lombok 🌶 추가

### @AllArgConstructor 어노테이션을 통한 DI
``` java
@Service
@AllArgConstructor
public class MemberService{

  private MemberDao memberDao;
}

``` 

### 불변성(Immutability) 지키기 위한 @RequiredArgConstructor 어노테이션을 통한 DI
❗ 이 경우 반드시 필드는 **final** 로 선언되어야한다. 
``` java
@Service
@RequiredArgConstructor
public class MemberService{

  private final MemberDao memberDao;
}

```