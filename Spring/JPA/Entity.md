# Entity, 영속성
> 여러 분야에서 각자의 역할 및 의미에 따라 달리 사용되는 용어지만,   
> JPA 환경에 한정하여 찾아본 정보를 정리해보았다.

```java
@Entity
@Table(name="user")
public class Member {

  @Id @GeneratedValue
  @Column(name="user_id")
  private Long id;

  private STring name;
}

```
JPA 의존성을 추가하고 **@Entity** 룰 붙인 클래스는 테이블과 자동적으로 매핑이 된다.   
➡ 하나의 엔티티 타입을 생성한다 == 하나의 클래스를 생성한다.

## 엔티티 클래스 관련 어노테이션
### @Id
 - 해당 컬럼이 식별키(PK; Primary Key)임을 나타낸다.
 - 모든 엔티티에 반드시 지정해야한다.
 - 주로 **@GenerateValue**와 함께 PK를 어떤 전략으로 생성하는지 명시

### @GeneratedValue
 - stratagy 속성과 generator 속성으로 구분
 - strategy
    - AUTO : 특정 테이블에 맞게 자동으로 생성
    - TABLE : 별도의 키를 생성해주는 테이블을 이용
    - SEQUENCE : DB의 시퀀스를 이용하여 PK 생성(Oracle에서 사용)
    - IDENTITY : 기본기 생성 방식 자체를 DB에 위임
 - generator
    - @tableGenerator, @SequnceGenerator

### @Column
  - JPA의 인스턴스 변수는 바로 컬럼이 된다 ➡ 별도의 컬럼명, 사이즈, 제약조건을 추가 / 지정하기 위해 사용

### @Table
  - JPA에선 클래스가 테이블이 되기떄문에 클래스 선언부에 작성하여 테이블명을 지정, 기본값은 클래스 이름으로 테이블 생성

### @Entity 
  - 해당 클래스의 인스턴스들의 엔티티임을 명시

[[참조출처 : 엔티티(Entity)]](https://velog.io/@jayjay28/%EC%97%94%ED%8B%B0%ED%8B%B0Entity)