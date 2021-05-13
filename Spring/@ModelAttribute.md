# @ModelAttribute

> 작성한 코드는 김영한님의 강의 <스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술> 의 내용에서 일부 발췌하였습니다.   
> 문제가 될 경우 해당 게시글은 삭제됩니다.

## 원리 🔎
1. 매개 변수로 오는 클래스의 객체를 생성   
2. 요청 파라미터의 이름으로 객체의 이름을 찾고 해당 프로퍼티의 setter를 호출하여 값을 입력    
ex) 파라미터의 이름이 username일 경우 -> setUsername()을 찾아 호출하여 값을 입력.

## 프로퍼티
어떤 객체에 getXXX(), setXXX() 메소드가 있다 == 해당 객체는 'XXX'라는 프로퍼티를 가진다.
ex) username의 값 변경 시 setUsername()이 호출, 조회 시엔 getUsername()이 호출된다.

## 예외 🚨
해당 객체의 필드와 맞지 않은 타입이 올 경우 'BindException'이 발생한다.

## 특징
@RequestParam과 같이 생략이 가능하다

### 주의사항 ❗
생략 시 스프링이 인식하는 방식
String, int(Integer) 같은 단순 타입 => @RequestParam
그 외 요소들 => @ModelAttribute

### 특이점 👀
@RequestBody 생략 시 ModelAttribute가 작동. 요청 파라미터가 존재하지 않을 경우 각각 null, 0 출력

``` java
@ResponseBody
@PostMapping("/~~~~~~")
public String requestBody(Member member) throw IOException{
  log.info("username={}, age={}", member.getUsername(), member.getAge());
  
  return "ok";
}

```