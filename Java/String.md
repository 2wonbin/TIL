# String a = "b" vs new string("b")
대화 도중에 String a = ~~ 와 String a = new String(~~)가 완전히 같지 않다는 사실을 알게되었다.

리터럴을 이용한 변수 할당은 내부 string (constant) pool에 저장 <br/>
문자열 객체를 만들어 변수를 할당하면 내부 heap 영역에 저장된다.<br/>

두 문자열 사이의 값은 같을지 몰라도, 참조하고 있는 주소가 다르다.

``` java
public class StringExam {

	public static void main(String[] args) {
		
		String a = "안녕";
		String b = new String("안녕");
		
		System.out.println(a == b);			//false
		System.out.println(a.hashCode());	//1611021
		System.out.println(b.hashCode());	//1611021
		System.out.println(a.equals(b));	//true 
	}
		
}
```
[참조출처](https://velog.io/@dltlsgh5/new-String%EA%B3%BC-String-str-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

문자열 객체를 만들어 생성하면 만들 때 마다 객체가 새로 등록되지만, <br/>
리터럴 변수 할당은 같은 값으로 만들 경우 같은 string pool에서 참조하므로 객체 생성은 한 번만 이루어진다.