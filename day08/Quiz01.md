### day08.Quiz01
>< 제어문 최종 문제 - 구구단 게임 만들기 >   
>   	1. 사용자에게 원하는 판 수를 입력 받는다.   
>    	2. 입력 받은 판 수 만큼 구구단 문제를 낸다.   
>    	3. 정답 시 100점, 오답일 경우 -10점.   
>    	4. 모든 횟수가 종료되면 총점을 출력한다.   
>    	5. 정답률을 퍼센티지로 출력한다.(소숫점은 생략한다.)   
>    	6. 정답률이 80% 이상이면 "win"을, 그렇지 않으면 "lose"를 출력한다.   
> 		7. jop활용   
   
```java
package day08.quiz;

import javax.swing.JOptionPane;

public class Quiz01 {
	public static void main(String[] args) {
		int point = 0;
		int pan = 0;
		int count = 0;
		String span = JOptionPane.showInputDialog("원하는 판 수를 입력하세요.");
		pan = Integer.parseInt(span);

		for (int i = 1; i <= pan; ++i) {
			int num1 = (int) (Math.random() * 8) + 2;
			int num2 = (int) (Math.random() * 9) + 1;
			String sAns = JOptionPane.showInputDialog(num1 + " x " + num2 + " = ?");
			
			int ans = Integer.parseInt(sAns);
			if (ans == num1 * num2) {
				point += 100;
				++count;
				continue;
			}
			point -= 10;
		}

		JOptionPane.showMessageDialog(null, "총점 : " + point);
		JOptionPane.showMessageDialog(null, "정답률 : " + ((double) count / pan) * 100 + "%");
		JOptionPane.showMessageDialog(null, ((double) count / pan * 100) >= 80 ? "WIN" : "LOSE");
	}
}
```
