### day10.homework01용 클래스 파일

```java
package day10.homework;

import javax.swing.JOptionPane;

public class Pokemon {
	String name;
	int hp, atk, lv;

	void input() {
		String nameInput = "이름을 입력하세요";
		name = JOptionPane.showInputDialog(nameInput);
		while(true) {
			lv = Integer.parseInt(JOptionPane.showInputDialog("레벨을 입력하세요"));
			if(0 < lv && lv < 100) {
				break;
			}
			else {
				JOptionPane.showMessageDialog(null, "1 ~ 99사이의 값을 입력하세요");
			}
		}
		hp = 1000 * lv;
		atk = lv * ((int)(Math.random() * 5)+1 == 1 ? 3 : 2);
	}
	
	

	void printInfo() {	// 처음에 문제 몰랐을때 만들었던 필요없는 메소드
		JOptionPane.showMessageDialog(null,"이름 : " + name + "\n레벨 : " + lv
                                                 + "\n체력 : " + hp + "\n공격력 : " + atk);
	}
		
}
```
