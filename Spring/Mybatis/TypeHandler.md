# TypeHandler, 타입 핸들러
> Java와 Database간 값이 옮겨다닐 때 자료형이 달라서 서로 호환이 되지 않는 경우가 발생한다.    
> 이럴때 스프링과 마이바티스에서 제공하는 TypeHnadler를 사용해 해당 문제를 해결해보자.


## 한 개의 Setter 메소드와 3개의 Getter 메소드를 내장

``` java
@MappedTypes(java자료형.class)
@MappedJdbcTypes(JdbcType.db자료형) 
public class TypeHandler extends BaseTypeHandler<java자료형>{   //BaseTypeHandler를 상속받는 클래스

  @Override
	public void setNonNullParameter(PreparedStatement ps, int i, (java자료형) parameter, JdbcType jdbcType)
			throws SQLException {

        int i = PreparedStatement의 '?' 자리 인덱스
        parameter = 해당 java 값
		
	}

	@Override
	public (java자료형) getNullableResult(ResultSet rs, String columnName) throws SQLException {
		
		String x = rs.getString(columnName);
		return x를 가지고 결과값 도출
	}

	@Override
	public (java자료형) getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
		String x = rs.getString(columnIndex);
		return x를 가지고 결과값 도출
	}

	@Override
	public (java자료형) getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
		String x = cs.getString(columnIndex);
		return x를 가지고 결과값 도출
	}
}

```

## mabatis-cofig.xml에 등록되어 있어야 적용된다.
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!-- environment, mapper 태그들은 앞으로 application-context.xml에서 관리 -->
	<typeHandlers>
		<typeHandler handler="com.kh.spring.common.typehandler.StringArrayTypeHandler"/> <!-- 직접 경로를 설정하는 방법 -->
		<package name="com.kh.spring.common.typehandler"/>                                <!-- 상위 패키지를 설정하여 내부 typehandler를 모두 등록 -->
	</typeHandlers>
</configuration>

```