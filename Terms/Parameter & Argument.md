# 매개변수와 전달인자
> 너무 기초적이지만 매번 헷갈리는 용어들을 따로 기록합니다.<br/>
> 원 소스를 그대로 복사 / 붙여넣기 하지 않아 내용에 오류가 있을 수 있습니다.

## 매개변수 (Parameter)
함수(메소드) 정의 단계에서 전달 받는 값
``` java
public void print(Sting name){  // 여기서 name이 매개변수(Parameter)
  Sysyem.out.println(name + "님 반갑습니다.");
}
```

## 전달인자(Argument)
함수(메소드) 선언 단계에서 대입되는 값
``` java
print("홍길동");
// print 메소드의 매개변수 자리에 실제로 들어가게 되는 값("홍길동")
```

