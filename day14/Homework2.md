### day14.Homework02(lastIndex를 지역변수로 선언한 경우)
#### -> main에서 lastIndex를 조절해준다
> Tourist 클래스   
>    필드 : name, budget(예산), destination(목적지)   
>    메서드 : 생성자 여러개 ...    
>    		getter, setter, ...   
>    		public String toString()    
>       
>  Quiz01 클래스 - main()   
>  	메뉴)    
>  		1. 목적지 설정   
>  		2. 여행객 추가    
>  		3. 모든 여행객 정보 보기   
>  		4. 전체 예산 보기   
>  		5. VIP 조회    
>  		0. 종료    
>     
>   여행객은 최대 5명까지 받는다.   
>   모든 여행객의 목적지는 동일하다.    
>   예산이 가장 많은 여행객이 VIP다.   

#### class Homework01
```java
package day14.homework;

import javax.swing.JOptionPane;
   
public class Homework01 {
	
	public static void main(String[] args) {
		Tourist[] tourists = new Tourist[5];
		Menu m = new Menu();
		int lastIndex=-1;
				
		String menu = "1. 목적지 설정\n2. 여행객 추가\n3. 모든 여행객 정보 보기\n4. 전체 예산 보기\n	5. VIP 조회\n	0. 종료";
		while(true) {
			String menuInput = JOptionPane.showInputDialog(menu);
			switch(menuInput) {
			case "1" : {
				m.menu1(lastIndex);
				break;
			}
			
			case "2" : {
				if(lastIndex==5) {
					JOptionPane.showMessageDialog(null, "더이상 추가할 수 없습니다");
					break;
				}
				++lastIndex;
				m.menu2(tourists, lastIndex);
				break;
			}
			
			case "3" : {
				m.menu3(tourists, lastIndex);
				break;
			}
			
			case "4" : {
				m.menu4(tourists, lastIndex);
				break;
			}
			
			case "5" : {
				m.menu5(tourists, lastIndex);
				break;
			}
			
			case "0" : {
				return;
			}
			
			default : {
				JOptionPane.showMessageDialog(null, "올바른 값을 입력하세요");
			}
							
			}//switch
		}//while
	}//메인
}//클래스
```
### class Tourist
```java
public class Tourist {
	private String name;
	private int budget;
	private static String destination;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getBudget() {
		return budget;
	}
	public void setBudget(int budget) {
		if(budget < 0) {
			return;
		}
		this.budget = budget;
	}
	public String getDestination() {
		return destination;
	}
	public static void setDestination(String destination) {
		Tourist.destination = destination;
	}
	
	void setInfo (String name, int budget, String destination) {
		setName(name);
		setBudget(budget);
		setDestination(destination);
	}
	
	
	public String toString() {
		return "이름 : " + this.name + ", 예산 : " + this.budget + ", 목적지 : " + Tourist.destination;
	}
			
}
```
### class menu
```java
public class Menu {
	
	public void menu1(int lastIndex) {
		if( lastIndex == -1 ) {
			JOptionPane.showMessageDialog(null, "여행객 정보가 없습니다");
			return;
		}
		String destination = JOptionPane.showInputDialog("목적지를 입력하세요");
		Tourist.setDestination(destination);
	}
	
	public void menu2(Tourist[] tourists, int lastIndex) {
		if( lastIndex >= 5 ) {
			JOptionPane.showMessageDialog(null, "더이상 추가할 수 없습니다");
			return;
		}

		String name = JOptionPane.showInputDialog("이름");
		int budget = Integer.parseInt(JOptionPane.showInputDialog("예산"));				
		String destination = JOptionPane.showInputDialog("목적지");
		tourists[lastIndex] = new Tourist();
		tourists[lastIndex].setInfo(name, budget, destination);
	}
	
	public void menu3(Tourist[] tourists, int lastIndex) {
		if( lastIndex == -1 ) {
			JOptionPane.showMessageDialog(null, "여행객 정보가 없습니다");
			return;
		}
		String touristInfo = "==== 모든 여행객 정보 ====\n";
		for(int i=0; i<=lastIndex; ++i) {
			touristInfo += tourists[i].toString() + "\n";
		}
		JOptionPane.showMessageDialog(null, touristInfo);
	}
	
	public void menu4(Tourist[] tourists, int lastIndex) {
		if( lastIndex == -1 ) {
			JOptionPane.showMessageDialog(null, "여행객 정보가 없습니다");
			return;
		}
		int totalBudget = 0;
		for(int i=0; i<=lastIndex; ++i) {
			totalBudget += tourists[i].getBudget();
		}
		JOptionPane.showMessageDialog(null,"전체 예산 : " + totalBudget);
	}
	
	public void menu5(Tourist[] tourists, int lastIndex) {
		if( lastIndex == -1 ) {
			JOptionPane.showMessageDialog(null, "여행객 정보가 없습니다");
			return;
		}
		int vipIndex=0;
		for(int i=1; i<=lastIndex; ++i) {
			if(tourists[vipIndex].getBudget() < tourists[i].getBudget()) {
				vipIndex = i;
			}
		}
		JOptionPane.showMessageDialog(null,"VIP회원 : " + tourists[vipIndex].getName());
	}
	
}
```
