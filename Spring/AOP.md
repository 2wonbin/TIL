# AOP (Aspect Oriented Programming; 관점 지향 프로그래밍)

> 개념은 '아~' 싶다가도 막상 구현하려고 하면 무슨 말인지, 무슨 일을 하는지, 어떻게 동작하는지 도대체 한 눈에 들어오지 않는다.<br/>
> 나름의 이해한 방식으로 정리해보도록 한다.

## 필요성
 - 부가기능(인프라 로직)은 애플리케이션 전 영역에서 나타남 > 중복코드(기능) 발생 가능성 🔺
 - 업무로직과 같이 있으면 업무 로직 이해에 어려움

## 용어 
 - Target : '어떤 대상'에 부가기능을 부여할 것인가.
 - Advice : 어떤 '부가 기능' : Before, AfterReturning, AfterThrowing, After, Around
 - JointPoint : '어디에' 적용할 것인가. 메소드 / 필드 / 객체 / 생성자 ....
 - PointCut : 실제 Advice가 적용될 지점(메소드)

[참조 : [10분 테코톡] 🌕제이의 Spring AOP](https://youtu.be/Hm0w_9ngDpM)

## Advice

- Before : joinpoint에서 메소드 **실행 전** 실행
- AfterReturning : joinPoint에서 메소드 **성공** 후 실행
- AfterThrowing : **예외발생**시 실행( ref)java의 catch 절)
- After : 메소드 **실행결과와 상관없이** 무조건 실행 ( cf)java의 finally절)
- Around : **모든** 시점에서 실행된다.

### 💫 Around는 양방향(왕복의 느낌)이라면 After는 단방향(돌아오는 편도의 느낌). (이랄까..)

## AOP 구현
> 먼저 AOP관련 의존성이 주입되어 있어야한다.

1. 선언적 AOP 구현
``` xml 
	<beans:bean id="loggerAspect" class="com.kh.spring.common.aop.LoggerAspect" /> Bean으로 등록할 클래스 지정
		<aop:config>	STS기준) XML 하단 namespaces탭에서 aop 체크해야 사용 가능 
		<aop:aspect id="loggerAspect" ref="loggerAspect">
			<aop:before method="beforeAdvice" pointcut-ref="loggerPointcut"/> <- aop 어드바이스(실행위치) 지정 | ref : pointcut id와 연결
			<aop:around method="aroundAdvice" pointcut-ref="loggerPointcut"/>	
			<aop:pointcut expression="execution(* com.kh.spring.memo..*(..))" id="loggerPointcut"/> 표현식과 id지정
		</aop:aspect>
	</aop:config>
```
2. Annotaition 방식 구현
``` xml
    <!-- maven 기준 servlet-context에 등록되어있어야한다. -->
	 <aop:aspectj-autoproxy />
```
``` java
@Component  //필수 Annotation
@Aspect     //필수 Annotation
public class LoggerAspect {
	
	@Pointcut("execution(* com.kh.spring.memo..*(..))")
	public void pointcut() {}

	@Around("pointcut()")   //advice 지정 후, pointcut 지정
	public Object aroundAdvice(ProceedingJoinPoint joinPoint) throws Throwable {
		Signature signature = joinPoint.getSignature();
		
		//joinPoint 실행 전 처리
		log.debug("[Before] {}", signature);
		
		Object obj = joinPoint.proceed();
		
		//joinPoint 실행 후 처리
		log.debug("[After] {}", signature);		
		
		return obj;
	}
}

```

## Pointcut Expression
 - 선언식
 <aop:pointcut expression="execution(표현식)>
 - Annotaion
 @Pointcut("execution("표현식"))

 ### 표현식 형식
 **(접근제한자) 리턴값 패키지주소 클래스명 메소드명(매개변수)**
 ``` java
 * com.kh.spring.memo..*(..))
 모든 자료형 리턴 / com.kh.spring.memo 패키지 / 이하 모든 클래스 / 모든 매소드 / 모든 파라미터
 ```

## AOP 구현방식
1. 컴파일
2. 바이트코드
3. 프록시