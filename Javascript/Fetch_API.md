# Fetch API
> 자바스크립트 비동기 통신(AJAX)를 지원하는 내장 API

``` javascript
let promise = fetch(url, option);

```
**url**에는 접근을 원하는 주소를, **option**에는 선택 매개변수, 대표적으로 header 설정, method, body 설정 등이 온다.
## chapter 1
요청 즉시 **promise** 객체 반환 -> 내장 클래스 response의 인스턴스와 함께 이행처리
  --> body가 도착하기 전이지만 이 단계에서 응답 헤더를 통해 요청의 성공 여부등을 확인하는 것이 가능.

## chapter 2
응답 본문을 확인 : response에는 promise를 기반으로 하는 메소드들이 존재 
- response.text() : 응답을 text로 변환
- response.json() : 응답을 JSON 형식으로 파싱

그 외에도 formData(), blob(); binary 형태로 변환 .. 등 이 있다.
