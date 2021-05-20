# 동적 SQL
[참조출처](https://mybatis.org/mybatis-3/ko/dynamic-sql.html)
- if
- choose(when | otherwise)
- trim, where, (set)
- foreach

## if

다른 언어들과 마찬가지의 용도로 특정 조건 시 실행할 구문을 내부에 작성한다.

```xml
<if test="searchKeyword != null and searchKeyword != ''">
	${searchType} like '%' || #{searchKeyword} || '%'	<!-- ''없이 불러오는 ${식별자} -->
</if>
<if test="gender != null and gender != ''">
	and gender = #{gender}
</if>
```

**주의사항**

- if태그 안에선 _and_ , _or_ 만 사용 가능하다. '&&', '||'는 사용할 수 없다.
- else 구문이 따로 없어 조건마다 if태그를 생성해야 한다.

<br/>

## choose

자바 switch문과 원리가 거의 똑같다. 특정 조건이 여러개일 경우 사용한다.

```xml
<if test="salary != null and salary != '' ">
	<choose>
		<!-- <![CDATA[....]]> : CDATA 내부 ....은 xml파일 내부에서도 문자열로 처리 -->
		<when test="salaryCompare eq 'le'"><!--  기본 처리절 -->
			and salary <![CDATA[<=]]> #{salary}
		</when>
		<when test="salaryCompare eq 'ge'"><!--  기본 처리절 -->
			and salary <![CDATA[>=]]> #{salary}
		</when>
		<otherwise></otherwise> <!-- defalut 처리절 -->
	</choose>
</if>
```

**주의사항**

- '<=' 같이 코드 내부에서 다른 처리가 들어가는 요소들은 '<!CDATA[요소]>' 를 이용하여 입력값 그대로 문자열 처리할 수 있도록 한다.
- else 구문이 따로 없어 조건마다 if태그를 생성해야 한다.

## trim, where, set

### &lt;where>

sql 구문의 where절에 위치하며, 아래의 규칙을 따른다.

1. where절 몸통이 비어있다면, where 키워드 제거
2. where 다음에 바로 and or가 온다면 제거

```xml
<where>
    <if test="state != null">
         state = #{state}
    </if>
    <if test="title != null">
        AND title like #{title}
    </if>
    <if test="author != null and author.name != null">
        AND author_name like #{author.name}
    </if>
  </where>
```

### trim

where가 원하는대로, 그러니까 and나 or을 그대로 인식한다면 trim으로 요소를 정의할 수 있다.

```xml
<trim prefix="WHERE" prefixOverrides="AND | OR ">
<!-- prefix로 선언한 where 내부 prefixOverrides의 value로 지정한 요소들을 삭제한다  -->
<!-- 추가하고 싶으면 width="추가 요소" --/>
  ...
</trim>
```

## foreach
``` xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}	<!-- (item[0], item[1]....)-->
  </foreach>
</select>
```

내부 요소들을 item의 이름으로 지정하고, 요소의 순서(위치)는 index로 지정한다.    
받아올 collection을 명시하고 Map, Set, List등 반복 가능한 객체를 파라미터로 전달할 수 있다.   
open에 지정한 요소로 시작하고, close에 지정한 요소로 마지막 반복 후 해당 설정 값으로 마무리 된다.   
구분자는 seperator로 지정한다.