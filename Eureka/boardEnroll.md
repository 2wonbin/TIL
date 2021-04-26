# 210426 실습문제 : boardEnroll

```
@실습문제: /board/boardEnroll.do 구현하세요. (첨부파일 없음)
- /board/boardForm.do, /board/boardEnroll.do 는 login한 상태에서만 접근할 수 있어야 합니다.
```

## 인터셉터를 사용한 login 유효성 검사
### servlet-context.xml 파일에 Interceptor Bean 등록
``` xml
<!-- #9. handler interceptor 등록 -->
<interceptors>
  <interceptor>
	<!-- mapping tag는 여러개 작성할 수 있다. -->
		<mapping path="/board/**/*.do"/>
		<exclude-mapping path="/board/boardList.do"/>   <!-- 인터셉터의 해당 경로 접근을 막는다 -->
	  <beans:bean id="loginInterceptor" class="com.kh.spring.common.interceptor.LoginInterceptor" />
	</interceptor>
</interceptors>
```

## 커맨드 객체를 이용한 사용자 입력값 저장
``` java
@PostMapping("/boardEnroll.do")
public String boadrEnroll(@ModelAttribute Board board, RedirectAttributes redirectAttributes) {
	log.info("board={}", board);
		
	try {
	int result = boardService.boardEnroll(board);
		
	String msg = "게시글 등록 성공!";
	redirectAttributes.addFlashAttribute("msg", msg);
	} catch (Exception e) {
		log.error("게시글 등록 오류!", e);
		throw e;
	}
	return "redirect:/board/boardList.do";
}
```

## mapper 파일에 query 작성
``` xml
<insert id="boardEnroll">
	insert into
		board
	values(
		seq_board_no.nextval,
		#{title},
		#{memberId},
		#{content},
		default,
		default
		)
</insert>
```
### ❗주의 : mybatis-config 파일에 mapUnderscoreToCamelCase -> true 여부 확인

```xml
<configuration>
	<settings>
    <!-- DB컬럼에서 넘어온 값을 자바의 카멜케이싱으로 처리, 기본값 false-->
		<setting name="mapUnderscoreToCamelCase" value="true"/>	
	</settings>
</configuration>
```