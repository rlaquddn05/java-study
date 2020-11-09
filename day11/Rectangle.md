###Quiz02 메소드 생성 클래스
```java
package day11.quiz;

public class Rectangle {
	int base;
	int height;
	
	void setData(int a, int b) {
		base = a;
		height = b;
	}
	
	int getArea() {
		return base*height;
	}
	
	int getCircum() {
		return 2*base + 2*height;
	}
}
```
