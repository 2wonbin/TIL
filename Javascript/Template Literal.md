# Template Literal

ES6에 추가된 자바스크립트 문법으로 \``(백틱)안에 오는 복합 문자열을 그대로 출력할 수 있게한다.<br/>
개행과 띄어쓰기도 인식한다.<br/>
외부에서 값을 불러올 땐 *${변수}*를 ``내부에 선언하여 사용한다. 

```javascript
function before(word) {
  console.log("입력한 단어는" + word + "입니다"); // 이전엔변수와 문자열을 분리했어야했다.
}

//ES6(ES2015)
function after(word) {
  console.log(`
  입력한 단어는 
  ${word}
  입니다.`);  // 개행문자를 그대로 출력한다.
}
```

<hr/>

## JSP, EL과 같이 사용할 경우 + etc

```jsp
function devSubmit(id){
		$("#devFrm")
		.attr("action", `${pageContext.request.contextPath}/demo/\${id}.do`)	// jsp에서 Teamplate literal은 '\'를 통한 escaping 처리
		.submit();
	}
```
JSP의 EL 태그도 ${}을 사용하여 값을 불러오고, 자바스크립트 Template Literal도 그러하다.<br/>
이 경우 '\' 키워드로 escaping 처리를 하여 다르게 인식하도록 하였다.
<br/>

위의 마크다운 양식에서도 백틱을 쓰면 어떤 처리가 진행되는 걸 발견하였다. 마찬가지로 '\'를 붙여 사용하니 일반 문자처럼 인식하였다.