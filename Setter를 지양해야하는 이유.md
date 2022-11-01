## Setter를 사용하면 안되는 이유<br>
* Setter 메소드를 사용하면 값을 변경한 의도를 파악할 수 없다.<br>
```
public Member updateMember(long id) {
    final Member member = findById(id);
    member.setFistName("value");
    member.setLastName("value");
    member.setAge("value");
    return member;
}
```
위의 코드를 봤을대 setter만으로는 어떤 의도로 데이터를 변경하는지 명확히 알 수 없다.<br>

* 객체의 일관성을 유지하기 어렵다.<br>
Setter는 public으로 언제든지 변경할 수 있는 상태가 된다. 위에 예시처럼 updateMember 메소드
뿐만 아니라 모든 곳에서 회원의 이름을 변경할 수 있기 때문에 일관성을 유지하기 어렵다.<br>

## Setter 대신 사용할것<br>
* 생성자 오버로딩
```
public class Member {
    private String name;
    private String age;
    
    public Member(String name){
    	this.name = name;
    }
    public Member(String name,int age){
    	this.name = name;
    	this.age = age;
    }
```
* Builder 패턴<br>
```
public class Member {
    private String name;
    private String age;
    
    @Builder
    public Member(String name, int age){
    	this.name = name;
        this.age = age;
    }
```
빌더패턴은 요구사항에 맞게 필요한 데이터만 이용하여 유연한 클래스 생성이 가능하다. 
때문에 다양한 생성자들이 사라지고 전체 생성자 하나만을 가지고 있는 형태로 변경되어
유지보수 및 가독성이 향상된다. 또한 객체를 생성할 때 인자 값의 순서가 상관없다는 장점이 있다.
* 정적 팩토리 메소드<br>
```
public class Member {
    private String name;
    private String age;
    
    public static void createMember(String name, int age){
    	this.name = name;
        this.age = age;
    }
    public static void createMemberName(String name){
    	this.name = name;
    }
```
정적 팩토리 메서드를 사용한다면 이름을 가질 수 있기 때문에 반환될 데이터를 추측할 수 있다.