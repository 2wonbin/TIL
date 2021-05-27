# Mybatis 사용 시 order by 정렬
> 최신순, 인기순 등 where 절이 아닌 order by(정렬)의 순서를 지정해야 하는 문제가 발생하였다.   
> 이 경우엔 어떻게 해야 하나.

## trim 태그를 씁시다.
``` xml

<select id="example" resultMap="exampleMap">
...
<trim prefix="ORDER BY">
  <if test='option.equals("recent")'> enroll_date DESC </if>
  <if test='option.equals("likes")'> like ASC</if>
</trim>
...
</select>
```

trim 태그의 prefix 접두어 요소로 order by를 지정하고,   
받아 온 자바코드의 검색 옵션을 설정하여, SQL문을 출력하도록 지정한다.
<hr />

## choose 태그를 씁시다. (21-05-27 추가)

``` xml
<choose>
  <when test='option.equals("recent")'>
    order by
     enroll_date DESC
  </when>
  <when test='option.equals("likes")'>
    order by
      like ASC
  </when>
  <otherwise> <!-- default 조건 -->
    order by
     blabla DESC
  </otherwise>
</choose>

```



[[Mybatis 동적 쿼리 정리]](https://github.com/2wonbin/TIL/blob/main/Spring/Mybatis/Dynamic-SQL.md)  <br />
[[참조출처 : order by 동적쿼리]](https://labj.tistory.com/472)