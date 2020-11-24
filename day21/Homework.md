### day21.Homework
> < 국가 관리 프로그램 >     
> 0. Nation 클래스     
> 	필드 : 국가명(nation)  수도명(capital)  인구수(population) ==> 모두 private     
> 	메서드 :     	
> 		Nation()     
> 		Nation(국가, 수도)    
> 		Nation(국가, 수도, 인구수)    
> 		getter, setter     
> 		toString() 오버라이드     
>     
> 1. ArrayList 객체 생성 (Nation 객체들을 저장할 창고 객체)     
>      	    
> 2. 메뉴 띄우기    
> 	1) 국가 추가   ==> 국가명, 수도명, 인구수 입력 받아 Nation 객체 생성 후 ArrayList에 add()    
> 	2) 모든 국가 보기	==> 현재 등록된 국가들을 모두 출력 (for문과 Nation.toString() 활용)    
> 	3) 국가 검색 	==> 국가명을 입력 받고, 해당 국가가 있으면 수도, 인구수 출력    
> 			    없으면 "미등록 국가"    
> 		            인구수는 ',' 추가 ( 예) 100,000,000 명 )     
> 	0) 종료 

```java
package day21.homework;

import java.text.DecimalFormat;
import java.util.ArrayList;

import javax.swing.JOptionPane;

class Nation {
	private String nation;
	private String capital;
	private int population;

	public Nation() {

	}

	public Nation(String nation, String capital) {
		this(nation, capital, 0);
	}

	public Nation(String nation, String capital, int population) {
		this.nation = nation;
		this.capital = capital;
		this.population = population;
	}

	public String getNation() {
		return nation;
	}

	public void setNation(String nation) {
		this.nation = nation;
	}

	public String getCapital() {
		return capital;
	}

	public void setCapital(String capital) {
		this.capital = capital;
	}

	public int getPopulation() {
		return this.population;
	}

	public void setPopulation(int population) {
		this.population = population;
	}

	@Override
	public String toString() {
		DecimalFormat df = new DecimalFormat("###,###");
		return "국가명 : " + getNation() + ", 수도 : " + getCapital() + ", 인구 : " + df.format(getPopulation()) + "\n";
	}

}

public class Homework01 {
	public static void main(String[] args) {
		ArrayList<Nation> nations = new ArrayList<Nation>();

		String menu = "1. 국가 추가\n2.모든 국가 보기\n3.국가 검색\n4.국가 제외\n0.종료";
		while (true) {
			String menuInput = JOptionPane.showInputDialog(menu).trim();
			switch (menuInput) {
			case "1": { // 올바르지 않은 국가명입력시 break 하고싶은데... 이건 국가명 풀을 상수로 인터페이스에 넣어야할거같은데.. 패스하겠습니다.
				String nation = JOptionPane.showInputDialog("국가명을 입력하세요 : ");
				if(nation == null) {
					break;
				}
				String capital = JOptionPane.showInputDialog("수도명을 입력하세요 : ");
				if(capital == null) {
					break;
				}
				int population = Integer.parseInt(JOptionPane.showInputDialog("인구수를 입력하세요 : "));
				nations.add(new Nation(nation, capital, population));
				break;
			}
			case "2": {
				if (nations.isEmpty()) {
					JOptionPane.showMessageDialog(null, "국가 추가를 먼저 하셔야 합니다");
					break;
				}
				String allNation = "";
				for (int i = 0; i < nations.size(); ++i) {
					allNation += nations.get(i);
				}
				JOptionPane.showMessageDialog(null, allNation);
				break;
			}
			case "3": {
				if (nations.isEmpty()) {
					JOptionPane.showMessageDialog(null, "국가 추가를 먼저 하셔야 합니다");
					break;
				}
				String input3 = JOptionPane.showInputDialog("검색할 국가명을 입력").trim();
				if(input3 == null) {
					break;
				}
				for (int i = 0; i < nations.size(); ++i) {
					if (input3.equals(nations.get(i).getNation())) {
						JOptionPane.showMessageDialog(null, nations.get(i));
						continue;
					}
					JOptionPane.showMessageDialog(null, "미등록 국가입니다");
				}
				break;
			}
			case "4" : {
				if (nations.isEmpty()) {
					JOptionPane.showMessageDialog(null, "국가 추가를 먼저 하셔야 합니다");
					break;
				}
				String input4 = JOptionPane.showInputDialog("제외할 국가명을 입력");
				if(input4 == null) {
					break;
				}
				for (int i = 0; i < nations.size(); ++i) {
					if (input4.equals(nations.get(i).getNation())) {
						nations.remove(nations.get(i));
					}
				}
				break;
			}
			case "0": {
				return;
			}
			default: {
				JOptionPane.showMessageDialog(null, "올바른 메뉴를 입력하세요");
			}
			}
		}
	}
}

```
