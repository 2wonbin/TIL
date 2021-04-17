# BigDecimal
찾아본 결과 많은 언어들이 소수의 계산을 정확하게 하지 못하는 문제를 겪는 걸 알게되었다. <br/>
그 개념적인 이유(부동소수점과 고정소수점의 차이 등) 까지 정확히 알 필요는 없어보였고 해결책만 기록해본다.<br/>

## 부동소수점 문제
``` java
/* 부동 소수점  문제*/
double a = 0.1;
double b = 0.2;
System.out.println(a+b);	
//원하는 값 0.3 / 출력 결과 : 0.30000000000000004
```

이 문제를 해결하기 위해 BigDecimal을 사용해보았다.
## BigDecimal : BigDecimal bigDecimal = new BigDecimal(param);
``` java
//BigDecimal bd = new BigDecimal("문자형"); 

//> 숫자도 인자로 받을 수 있지만 원하는 값이 나오지 않는다.		
//BigDecimal c = new BigDecimal(0.1);
//0.3000000000000000055511151231257827021181583404541015625

BigDecimal c = new BigDecimal("0.1");
BigDecimal d = new BigDecimal(String.valueOf(b));
		
//System.out.println(c+d);			//일반적인 사칙연산 적용X
System.out.println(c.add(d));		//더하기
System.out.println(c.subtract(d));	//빼기
System.out.println(c.multiply(d));	//곱하기
System.out.println(c.divide(d));	//나누기
```
[참조링크](https://wakestand.tistory.com/203)

## 기타 연산

``` java
/* 형 변환 */
		
int intBD = c.intValue();
long longBD = c.longValue();
float floatBD = c.floatValue();
double doubleBD = c.doubleValue();
String stringBD = c.toString();

/* 값 비교 : compareTo() 
크면 1, 맞으면 0, 작으면 -1(정수형 결과 리턴, 유리수는 반대) */
int result = c.compareTo(d);  //-1
System.out.println(result);
```
[참조링크](https://coding-factory.tistory.com/605)