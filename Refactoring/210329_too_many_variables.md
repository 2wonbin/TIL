# 변수가 많을 경우 어떻게 처리하지?
넥사크로 과제를 하는 도중 수많은 변수를 일일이 선언하고 있는 내 자신을 발견하게 됐다.
```javascript
  const major = this.Radio00;
  const password = this.Edit00_00;
  const name = this.Edit00_01;
  const id = this.Edit00;
  const phone = this.MaskEdit00;
  ```
  ```javascript
  this.Edit00.set_value("");
  this.Edit00_00.set_value("");
  this.Edit00_01.set_value("");
  this.Radio00.set_value("");
  this.MaskEdit00.set_value("");
  ```
  
  변수의 개수가 적을 땐 유효할지 모르겠지만 입력창이 20개, 100개가 넘어가면 그만큼 하나씩 선언 | 초기화를 해야하는 문제점이 발생한다.<br/>
  **이 경우엔 어떻게 해결해야 할까?**
  
