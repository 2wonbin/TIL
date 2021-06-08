# CORS(Cross Origin Resource Sharing)

``` html
Access to XMLHttpRequest at 'http://localhost:10000/springboot/menus' from origin 
'http://localhost:포트번호' has been blocked by CORS policy: 
No 'Access-Control-Allow-Origin' header is present on the requested resource. 
```
크롬 콘솔창에 해당 메시지가 나오면 CORS 정책에 위반된 경우이다

## CORS ❓

**도메인** 또는 **포트**가 다른 서버의 자원을 요청하는 매커니즘. 동일출처정책(SOP; Same-Origin-Policy, 비동기요청은 같은 origin으로만 요청을 보낼 수 있다.)에 의해 외부서버에 요청한 데이터를 브라우저 측에서 보안목적으로 차단한다.   
[[참조출처]](https://velog.io/@2_gyehong/CORS)

## 어떻게 해결하나요 ❓
### (스프링🌱 기준)
1. 응답Header에 **Access-Control-Allow-Origin**를 추가한다.

``` java
@GetMapping("/menus")
public List<Menu> menus(HttpServletResponse response){
  List<Menu> list = new ArrayList<Menu>();
  
  list = menuService.selectMenuList();			
  response.setHeader("Access-Control-Allow-Origin", "*");	//모든 사이트에 대해 CORS 허용
  return list;
	}
```

2. **@CrossOrigin** 어노테이션을 추가한다.

  ``` java
@CrossOrigin
@GetMapping("/menus")
public List<Menu> menus(HttpServletResponse response){
  List<Menu> list = new ArrayList<Menu>();
  list = menuService.selectMenuList();			

  return list;
}

```
