### day11.Quiz02
#### 메소드 생성 예제2
>  클래스 : Rectangle   
>   - 필드(멤버변수) : base, height   
>   - 메소드    
>     1) setData() : 두 정수를 인자값으로 받아, 객체의 base, height에 각각 저장   
>     2) getArea() : 넓이를 리턴   
>     3) getCircum() : 둘레를 리턴   
>     
>  메인 클래스 : Quiz02   
>   - Rectangle 객체 1개 생성    
>   - JOptionPane을 사용하여 밑변, 높이를 입력 받고,    
>     Rectangle 객체에 저장 (setData() 사용)   
>   - 이 사각형 객체의 넓이와 둘레를 메소드를 사용하여 출력 (getArea(), getCircum())   

```java
package day11.quiz;

import javax.swing.JOptionPane;

public class Quiz02 {
	public static void main(String[] args) {
		Rectangle rectangle = new Rectangle();
		int base = Integer.parseInt(JOptionPane.showInputDialog("밑변을 입력하세요"));
		int height = Integer.parseInt(JOptionPane.showInputDialog("높이를 입력하세요"));
		
		rectangle.setData(base, height);
		
		JOptionPane.showMessageDialog(null, "넓이 : " + rectangle.getArea() + 
										  "\n둘레 : " + rectangle.getCircum());	
				
	}
}
```
