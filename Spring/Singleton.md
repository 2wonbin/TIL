# 싱글톤(Singleton)
> 이 게시글엔 김영한님의 <스프링 핵심 원리 - 기본편>  강의 내용 일부가 포함되어 있습니다.<br />
> 문제가 될 경우 삭제합니다. 


Web Application은 여러 고객이 동시에 요청을 보낸다.<br />
그 말인 즉슨 요청마다 그만큼의 객체가 생성되고 소멸된다. -> 메모리 낭비 <br/>
## 싱글톤 패턴(Singleton Pattern)
인스턴스가 딱 1개만 생성되게 하는 디자인 패턴
``` java
// 클래스 내부
private static final SingletonEX intstance = new SingletonEX();
// static 영역에 객체 하나만 생성, 객체의 이름은 관레상 instance로 한다.

public static SingletonEX getInstance(){
  return instance;
  // public으로 설정, 객체 인스턴스 필요시 static 메소드를 통해서만 조회. getInstance 이름 역시 관례를 따라 표기하였다.
}

private SingletonEX(){
  //생성자를 private로 지정 -> 외부에서 new 키워드롤 통한 생성을 막는다.
}
```
## 싱글톤 컨테이너(Singleton Container)

싱글톤 패턴의 문제
 - 구현 코드 多
 - 구체 클래스에 의존(DIP 위반, OCP 위반)
 - 내부 속성 변경 및 초기화에 어려움.
 - private 생성자이므로 자식 클래스 생성 어려움
 - 외부 상황에 대처할 유연성이 떨어진다.

**따른 설정없이 스프링 컨테이너 내부에서 스프링 빈들은 모두 싱글톤으로 관리된다.**

## 싱글톤 방식의 주의점
여러 클라이언트가 같은 인스턴스를 공유.<br/>
== 싱글톤 객체가 상태를 유지하도록 설계하면 참조단계에서 오류가 발생한다.
 - 특정 클라이언트에 의존 X
 - 특정 클라이언트가 필드 값 변경하면 X
 - 가급적 read-only