## IoC(Inversion of Cotrol)<br>
���α׷��� �帧�� ���ΰ� �ƴ� �ܺο��� �����ϴ°�

IoC�� ������ �ȵ�����<br>
A: �ĸ���ġ��, ȣ�л�, ����ҽ��� �� ������ġ�� �ּ���<br>
B: �̹� ������ġ�� �ϼ��Ǿ� �־ ��Ḧ ������ �� �����ϴ�.<br>
���� ���ø� �ڵ�� ���캸�� ������ ����.
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
���� �ڵ�� ���� ������ġ�� ���°� �̹� �����Ǿ� ���� �ֹ��� �´� ������ġ�� ������� Ŭ������ ���� �����ؾ� �Ѵ�.<br><br>
IoC�� ���������<br>
A: �ĸ���ġ��, ȣ�л�, ����ҽ��� �� ������ġ�� �ּ���<br>
B: �� �˰ڽ��ϴ�.<br>
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
���� �ڵ�� ���� ������ġ�� ������ ������� ��Ḧ ���ڷ� �޾� ��ῡ ���� �������� �ܺο��� ���� �� �ִ�.


