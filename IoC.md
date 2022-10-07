## IoC(Inversion of Cotrol)<br>
프로그램의 흐름을 내부가 아닌 외부에서 제어하는것

IoC가 적용이 안됐을때<br>
A: 파마산치즈, 호밀빵, 돈까스소스가 들어간 샌드위치를 주세요<br>
B: 이미 샌드위치는 완성되어 있어서 재료를 선택할 수 없습니다.<br>
위의 예시를 코드로 살펴보면 다음과 같다.
```
public class Sandwich {
	WhiteBread whiteBread;
	MozzarellaCheese mozzarellaCheese;
	ChiliSauce chilliSauce;
	
	public Sandwich() {
		this.whiteBread = whiteBread;
		this.mozzarellaCheese = mozzarellaCheese;
		this.chiliSauce = chiliSauce;
	}
}
```
위의 코드와 같이 샌드위치의 형태가 이미 결정되어 고객의 주문에 맞는 샌드위치를 만들려면 클래스를 대폭 수정해야 한다.<br><br>
IoC가 적용됐을때<br>
A: 파마산치즈, 호밀빵, 돈까스소스가 들어간 샌드위치를 주세요<br>
B: 네 알겠습니다.<br>
```
public class Sandwich {
	Bread bread;
	Cheese cheese;
	Sauce sauce;
	
	public Sandwich(Bread bread, Cheese cheese, Sauce sauce) {
		this.bread = bread;
		this.cheese = cheese;
		this.sauce = sauce;
	}
}
```
위의 코드와 같이 샌드위치는 종류에 상관없이 재료를 인자로 받아 재료에 대한 결정권을 외부에서 가질 수 있다.


