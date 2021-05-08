# MYBATIS 내부 페이징 처리
```java
@GetMapping("/boardList.do")
public void boardList(@RequestParam(defaultValue = "1")int cPage, Model model, HttpServletRequest request) {
//현재 페이지(cPage)에 default 값 설정, 맨 첫 페이지가 '1'이 되도록.
	int numPerPage = 5;   /* 한 페이지에 표시할 게시글의 수*/
	Map<String,Object> param = new HashMap<>();
	param.put("numPerPage", numPerPage);
	param.put("cPage", cPage);
    /*Map 객체에 담아 DB까지 전달*/
	//a. contents 영역 : mybatis의 RowBounds
	List<Board> list = boardService.selectBoardList(param);
```
## MYBATIS ROWBOUND
페이지 당 게시물 수(numPerPage)를 **limit**로 <br/>
건너뛸 행의 수((현재 페이지; cPage - 1) * 페이지 당 게시물 수)를 **offset**으로 변수 지정   
**RowBounds** 객체를 생성하여 offset과 limit을 인자로 전달.
``` java
@Override
public List<Board> selectBoardList(Map<String, Object> param) {
	int cPage = (int)param.get("cPage");
	
	int limit = (int)param.get("numPerPage");
	int offset = (cPage - 1) * limit;	// 1->0, 2->5, 3->10,....
    RowBounds rowBounds = new RowBounds(offset, limit);
		
	return session.selectList("board.selectBoardList", null, rowBounds);
		
}
```

```java
		//b. pagebar 영역
		int totalContents = boardService.getTotalContents();
		String url = request.getRequestURI();
		String pageBar = HelloSpringUtils.getPageBar(totalContents, cPage, numPerPage, url);
//		log.info("pageBar={}", pageBar);
		//3. jsp 위임
		model.addAttribute("list",list);
		model.addAttribute("pageBar", pageBar);
	
	}
```