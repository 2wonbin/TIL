# 자바 옵셔널(Optional)

## 자바 8버전 이전 NULL을 피하는 방법 😎

null인 경우와 아닌 경우로 분기처리 
``` java

public void method(){
  if(blabla != null){
    excute1();
  }
  else{
    excute2();
  }
}

```

## Optional 클래스 ❓

Optional 클래스는 값이 있을 경우 값을 감싼다. 값이 없을 경우 **Optional.empty()** 메소드로 Optional 객체를 반환한다.    

[참조출처 : 모던 자바 인 액션 p.369]

## Optional 클래스의 객체 & 메소드
  - Optional.empty() : 비어있는 객체
  - Optional.of(객체) : null일 수 없는 객체
  - Optional.ofNullable(null 가능성이 있는 객체)
  
  결과
  - get() :T	, 객체가 null인 경우 NoSuchElemnetException을 throw -> null이 아님이 확실할 경우 사용
  - orElse(기본값): 객체가 null인 경우 기본값으로 처리
  - orElseGet(Supplier) : 객체가 null인 경우 supplier가 처리한 리턴한 값을 리턴
  - orElseThrow(exception supplier) : 객체가 null인 경우 exception supplier가 제공한 예외를 리턴 (일부로 예외 발생시)


