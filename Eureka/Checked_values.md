# 체크된 값 불러오기 (In javascript)

체크박스의 값이나 라디오 버튼으로 다중 선택된 값을 한꺼번에 불러오기 위해선 어떻게 해야할까.<br/>

### 예제
``` javascript
<div class="col-sm-10">
  <div class="form-check form-check-inline">
    <input class="form-check-input" type="checkbox" name="lang" id="Java" value="Java" ${dev.lang }>
    <label class="form-check-label" for="Java">Java</label>
  </div>
  <div class="form-check form-check-inline">
    <input class="form-check-input" type="checkbox" name="lang" id="C" value="C">
    <label class="form-check-label" for="C">C</label>
  </div>
  <div class="form-check form-check-inline">
    <input class="form-check-input" type="checkbox" name="lang" id="Javascript" value="Javascript">
    <label class="form-check-label" for="Javascript">Javascript</label>
  </div>
  <div class="form-check form-check-inline">
    <input class="form-check-input" type="checkbox" name="lang" id="Python" value="Python">
    <label class="form-check-label" for="Python">Python</label>
  </div>
</div>
```

## 바닐라 자바스크립트

``` javascript
const checkedList = document.queryselelctAll(input[속성값]:checked)  // 배열형태로 리턴
checkedList.forEach( e => console.log(e.value));
```

## Jquery
``` javascript
$("input:checked[속성값]:checked").each(function(){
  arr = $(this).val();
  console.log(arr);
  });
```
