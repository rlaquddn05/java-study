### day10.Homework01
>   Pokemon 클래스    
>       필드 : 이름, 레벨(int), 체력(int), 공격력(int)     
>     
>   Homework01 클래스     
>       메인메서드 :     
>          Pokemon 객체 5개짜리 배열 1개 만들기     
>          메뉴 (무한 while문 사용)     
>             1. 포켓몬 등록    
>             2. 모든 포켓몬 보기    
>             3. 레벨업    
>             0. 종료    
>          
>      1. 포켓몬 등록    
>         포켓몬 이름, 레벨을 입력 받고     
>          체력은 레벨의 1000배, 공격은 레벨의 2배 (20% 확률로 3배)     
>          ==> 5마리 한꺼번에 진행  혹은 1마리씩 진행     
>       2. 모든 포켓몬 보기    
>          배열에 담겨있는 모든 포켓몬의 모든 정보 출력    
>        3. 레벨업    
>          방법1. 배열에 담겨있는 모든 포켓몬의 레벨을 1 증가    
>          방법2. 인덱스 입력 받고 해당 포켓몬의 레벨을 1 증가    
>          방법3. 이름을 입력 받고 해당 포켓몬의 레벨을 1 증가    
>                (없는 이름인 경우 '미등록 포켓몬')     

```java
package day10.homework;

import javax.swing.JOptionPane;

public class Homework01 {
	public static void main(String[] args) {
		Pokemon [] pokemon;
		pokemon = new Pokemon[5];
		for(int i=0; i<pokemon.length;++i) {
			pokemon[i] = new Pokemon();
		}
		
		JOptionPane.showMessageDialog(null, "처음에 포켓몬을 생성하고 시작하여야 합니다.");
		for(int i=0; i<pokemon.length; ++i) {
			JOptionPane.showMessageDialog(null, i+1+"번 포켓몬의 정보를 입력하세요");
			pokemon[i].input();
		}
		
		String menu = "=========메뉴========="
				+ "\n          1. 포켓몬 다시 생성"
				+ "\n          2. 포켓몬 현황"
				+ "\n          3. 레벨업"
				+ "\n          4. 종료";
		while(true) {
			String menuInput = JOptionPane.showInputDialog(menu);
			switch (menuInput) {
				case "1" : {
					for(int i =0; i<pokemon.length; ++i) {
						JOptionPane.showMessageDialog(null, i+1+"번 포켓몬의 정보를 입력하세요");
						pokemon[i].input();
					}
					break;
				}
				
				case "2" : { // 처음에 문제 몰라서 잘못만든거 그대로 둠
//					String message = "어떤 포켓몬의 정보를 확인하시겠습니까?";
//					for(int i=0; i<pokemon.length; ++i) {
//						message += "\n"+ (1+i)+". " + pokemon[i].name;
//					}
//					message += "\n6. 전부";
//					int input2 = Integer.parseInt(JOptionPane.showInputDialog(message));
					String info = "";
//					if(input2 == 6) {
						for(Pokemon p : pokemon) {
							info += "이름 : " + p.name 
								 + "\n레벨 : " + p.lv 
								 + "\n체력 : " + p.hp 
								 + "\n공격력 : " + p.atk
								 + "\n--------------------------\n";
						}
						JOptionPane.showMessageDialog(null, info);
//					}
//					else if(1<=input2 && input2<=5) {
//						pokemon[input2-1].printInfo();
//					}
//					else {
//						JOptionPane.showMessageDialog(null, "1~6사이의 숫자를 입력하세요");
//					}
					break;
				}
				
				case "3" : {
					String lvUpName = JOptionPane.showInputDialog("레벨업할 포켓몬의 이름을 입력하세요");
					int nocount=0;
					for(Pokemon p : pokemon) {
						if (p.name.equals(lvUpName)) {
						++p.lv;
						JOptionPane.showMessageDialog(null, p.name + "의 레벨이 1 올라 " + p.lv + "가 되었다!");
						p.hp = 1000 * p.lv;
						String lvUpMessage = "                  <  "+p.name +"  >"
								+ "\n레   벨 : " + (p.lv-1) + " ====> " + p.lv
								+ "\n체   력 : " + (p.hp-1000) + " ====> " + p.hp
								+ "\n공격력 : ";	
							if(p.atk == 2*(p.lv-1)) {
							p.atk = 2 * p.lv;
							lvUpMessage += (p.lv-1)*2 + " ====> " + p.atk;
							JOptionPane.showMessageDialog(null, lvUpMessage);
							continue;
							}
							p.atk = 3 * p.lv;
							lvUpMessage += (p.lv-1)*3 + " ====> " + p.atk;
							JOptionPane.showMessageDialog(null, lvUpMessage);
						continue;
						}
						++nocount;									
					}
					if(nocount==5) {
						JOptionPane.showMessageDialog(null, "미등록 포켓몬 입니다.");
					}
					break;
				}
				
				case "4" :{
					return;
				}
				
				default : {
					JOptionPane.showMessageDialog(null, "1 ~ 4 사이의 값을 입력하세요");
				}
								
			} // switch			
	 	} // while		
	} //메인
} // 클래스
```
