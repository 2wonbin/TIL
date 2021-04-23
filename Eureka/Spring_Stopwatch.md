# 210423 실습문제 : Spring StopWatch

```
@실습문제 : Around Advice - insertMemo메소드의 실행시간을 구하시오.
스프링이 제공하는 org.springframework.util.StopWatch를 사용할 것.
```

## org.springframework.util.StopWatch
[참조](https://creamilk88.tistory.com/151) | [스프링문서](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/StopWatch.html)

Spring이 제공하는 StopWatch 클래스에 start()와 stop() 메소드를 사용 <br/>
그 사이의 차이를 getTotalTimeMillis()로 구한다.

``` java
package com.kh.spring.common.aop;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Component;
import org.springframework.util.StopWatch;

import lombok.extern.slf4j.Slf4j;

@Slf4j
@Component
@Aspect
public class Stopwatch {
	
	@Pointcut("execution(* com.kh.spring.memo.controller..insertMemo(..))")   //insertMemo 메소드를 가르키는 pointcut 표현식 작성
	public void pointcut() {}

	@Around("pointcut()")   //Around advice로 pointcut 실행
	public Object aroundAdvice(ProceedingJoinPoint joinPoint) throws Throwable{
		StopWatch stopwatch = new StopWatch();    // spring stopwatch 객체 생성
		stopwatch.start();                        // 시작
		
		Object obj = joinPoint.proceed();         //업무 실행
		
		stopwatch.stop();                         // 끝
		log.info("소요시간: {}", stopwatch.getTotalTimeMillis() + "ms"); 
    //INFO : com.kh.spring.common.aop.Stopwatch.aroundAdvice(Stopwatch.java:28) - 소요시간: 19ms 
    // start()와 stop() 실행 사이 소요시간 getTotalTimeMillis로 리턴.

		return obj;
	}
}
```
[AOP 정리](https://github.com/2wonbin/TIL/blob/main/Spring/AOP.md)
