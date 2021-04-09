# 동적 sql

- if
- choose(when | otherwise)
- trim, where, set
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
