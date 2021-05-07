# 부동소수점

많은 프로그래밍 언어가 소수의 연산을 계산하는데 어려움을 겪는다.<br/>
자바의 경우 BigDecimal 타입을 통해 해결해나간다.
[정리한 내용](https://github.com/2wonbin/TIL/blob/main/Java/BigDecimal.md)<br/>

자바스크립트의 경우 어떻게 처리할까?<br/>
간단하게 정수로 바꾼 후 실수로 다시 바꿔준다.
``` javascript
0.1 + 0.2 = 0.30000000000000004

(0.1 * 10 + 0.2 * 10) / 10 = 0.3
```
더 좋은 방법이 없을까 과연.