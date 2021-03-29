# 변수가 많을 경우 어떻게 처리하지?
넥사크로 과제를 하는 도중 수많은 변수를 일일이 선언하고 있는 내 자신을 발견하게 됐다.
```javascript
const major = this.Radio00;
const password = this.Edit00_00;
const name = this.Edit00_01;
const id = this.Edit00;
const phone = this.MaskEdit00;

const inputArr = [major, password, name, id, phone];
  for(let i = 0; i < inputArr.length; i++){
    f(inputArr[i].value == "" || inputArr[i].value == null){
      alert("비어있는 항목이 존재합니다.");
      inputArr[i].setFocus();
        return;
      } 
  }
  ```
  ```javascript
  this.Edit00.set_value("");
  this.Edit00_00.set_value("");
  this.Edit00_01.set_value("");
  this.Radio00.set_value("");
  this.MaskEdit00.set_value("");
  ```
  
  변수의 개수가 적을 땐 유효할지 모르겠지만 입력창이 20개, 100개가 넘어가면 그만큼 하나씩 선언 / 초기화를 해야하는 문제점이 발생한다.<br/>
  **이 경우엔 어떻게 해결해야 할까?**
  
  # 해결방안
  
공통된 속성을 찾아서 묶어내도록(grouping; ex.배열) 노력한다.
```javascript
for(let i=0; i<this.all.length; ++i) {
  if((this.all[i] instanceof nexacro.Edit || 
      this.all[i] instanceof nexacro.Radio ||
      this.all[i] instanceof nexacro.MaskEdit) &&
     (this.all[i].value == "" || this.all[i].value == null)) {			
       alert("비어있는 항목이 존재합니다.");
       this.all[i].setFocus();
        return;
       }
   }
```
```javascript
for(let i=0; i<this.all.length; ++i) {
  if(this.all[i] instanceof nexacro.Edit || 
     this.all[i] instanceof nexacro.Radio ||
     this.all[i] instanceof nexacro.MaskEdit) {		
      this.all[i].set_value("");
     }
 }
  ```
  
  예제의 경우 입력창의 자료형을 검사하여(**instance of**) 맞는 조건을 찾아내었다.<br/>
  특별한 경우가 아니면 id값을 알맞게 설정하거나, 다른 공통점을 찾아 값의 수가 늘어나도 알맞게 대응할 수 있도록 한다.
