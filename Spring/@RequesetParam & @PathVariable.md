# @RequestParam 과 @PathVariable

>  둘 다 url에 mapping된 parameter의 값을 불러오는데 사용하지만, 그 쓰임이 같지 않다고 생각해서 찾아보았다.

## 파라미터를 전달하는 두가지 경우 ✌

### 1.  GET 방식 요청 url
``` 
http://localhost:8080/cPage=1&keyWord="abc"
```
### 2. RESTful 요청 url
```
http://localhost:8080/board/1
```

### 1번 방식의 url에서 파라미터를 받아올 때 **@RequestParam**을 ,     2번 방식의 url에서 받아올 땐 **@PathVariable**을 사용한다.

## @RequestParam

``` java
@GetMapping("/url")
public void boardList(@RequestParam int cPage, @RequestParam String keyWord){
  ....
}
```
 - 해당 url에 전달받은 key 값으로 변수에 담는다.
 - 해당 값이 존재하지 않을 경우 400 관련 에러가 발생 --> 이 경우를 막기위해 *defaultValue*, *required=false*를 설정해 값이 들어오지 않아도 처리할 수 있도록 한다.

### 많은 파라미터 처리
``` java
@GetMapping("/url")
public void boardList(@RequestParam Map<Stirng, Object> param){

  String keyword = param.get("keyWord");
  int cPage = param.get("cPage");
  ...
}
```
Map 컬렉션을 사용해서 한번에 받아와, 설정된 key값으로 조회후 변수에 대입한다. --> 직관적이지 못해 *커맨드 객체*를 만들어 사용하는 것이 용이

## @PathVarible

``` java
@GetMapping("/board/{idx}")
@ResponseBody
public void boardList(@PathVariable("idx") int id){
  ....
}
```
 - 어떤 요청이든 하나 밖에 쓸 수 없다. 여러개의 요청을 받고 싶으면 **@MatrixVariable**을 사용한다

[[참조출처 : @RequestParam과 @PathVariable? ]](https://2ham-s.tistory.com/290)
[[참조출처 : @RequestParam과 @PathVariable 차이점 비교 ]](https://willbesoon.tistory.com/102)