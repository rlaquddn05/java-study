### day08.Homework10_2
#### jop활용

```import javax.swing.JOptionPane;

public class Homework10_2 {
	public static void main(String[] args) {
		int roomNo = Integer.parseInt(JOptionPane.showInputDialog("호텔의 방 갯수를 입력하세요: "));
		int[] hotel = new int[roomNo];
		
		while(true) {
		String menu = "==========메뉴==========\n"  
					+ "                 1. 체크인\n" 
					+ "                 2. 체크아웃\n" 
					+ "                 3. 현황 보기\n" 
					+ "                 0. 종료하기";
		String input = JOptionPane.showInputDialog(menu);
		String menu3="";
		for (int i=0;i<roomNo;i++ ) {
			menu3 += (i+1)+". 호 : " ;
			if(hotel[i]==0) {
				menu3 += "빈 방\n";
			}
			else {
				menu3 += "입실 중\n";
			}
		}
		
		switch (input) {
			case "1": {
				int menu1in = Integer.parseInt(JOptionPane.showInputDialog("원하시는 방 호수를 입력하세요."));
					if (hotel[menu1in - 1] == 0) {
					hotel[menu1in - 1] = 1;
					JOptionPane.showMessageDialog(null, "입실완료!");
					} 
				else {
					JOptionPane.showMessageDialog(null,"입실중인 방은 체크인 하실 수 없습니다.");
				}	
			break;
			}
			
			case "2": {
				int menu2in = Integer.parseInt(JOptionPane.showInputDialog("퇴실하시는 방 호수를 입력하세요."));
					if (hotel[menu2in - 1] != 0) {
					hotel[menu2in - 1] = 0;
					JOptionPane.showMessageDialog(null, "퇴실완료!");
					} 
				else {
					JOptionPane.showMessageDialog(null,"빈 방은 체크아웃 하실 수 없습니다.");
				}	
			break;
			}
			
			case "3": {
				JOptionPane.showMessageDialog(null, menu3);
				break;
			}
			
			case "0":{
				return;
			}
		}//스위치
		}//while
	}//메인
}// 클래스
```
