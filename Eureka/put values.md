# 값 대입
```html
<table id="ajaxSelectStudent" class="tbl-student">
 <tr>
  <th>학생번호</th>
  <td>
   <input type="number" name="no" readonly/>
  </td>
 </tr>
 <tr>
  <th>학생이름</th>
  <td>
   <input type="text" name="name" readonly/>
  </td>
 </tr>
 <tr>
  <th>학생전화번호</th>
  <td>
    <input type="tel" name="tel" readonly/>
  </td>
 </tr>
</table>
```
비동기 통신으로 얻은 값을 각각 input 타입의 value로 넣었어야 했다.
``` javascript
.....
success : function(data){
  console.log(data);
  if(data){
    var $table = $(ajaxSelectStudent);
    $table.find("[name=no]").val(data.studentNo);
    $table.find("[name=name]").val(data.studentName);
    $table.find("[name=tel]").val(data.studentTel);			
}
.....
```
-> find(속성값)을 통해 테이블 내부 input 태그에 접근하였다. 더 좋은 방법은 없을까?
