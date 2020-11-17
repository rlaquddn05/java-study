### day16 Homework
> < Sniper VS Tank >    
> - 저격수, 탱크 두 캐릭터 중 아무거나 랜덤하게 2개 생성   
>   (탱크 vs 탱크, 저 vs 탱, 저 vs 저)   
> - 두 객체가 서로 죽을 때까지 서로 공격을 반복   
> - 첫번째, 혹은 두번째 플레이어가 이겼는지 마지막 승자 출력!    
>  e.g. 플레이어1(탱크)의 승리!   

#### 1. 기본
```java
package day16.quiz;

class Unit { // 부모 클래스
	String name;
	int hp, att; // 체력, 공격력
	boolean alive; // true:아직 살아있음 (선택사항)
	
	public Unit() {}
	public Unit(String name) {
		this.name = name;
	}
	public Unit(String name, int hp, int att) {
		this.name = name;
		this.hp = hp;
		this.att = att;
		this.alive = true;
	}
	public void attack(Unit enemy) {
		
	}
	
	public boolean getAlive() {
		return hp > 0;
	}
}
class Sniper extends Unit { // 자식 클래스
	// 객체 생성되면, 자동으로 name은 "저격수", hp는 400, att는 100
	public Sniper() {
		super("저격수", 400, 100);
	}
	// attack 오버라이드 
	@Override
	public void attack(Unit enemy) {
		// 1. 10% 확률로 헤드샷 (상대 즉사)
		// 2. 나머지 확률로 평타(일반 공격, 상대 hp를 100만큼 깎는다.)
		if (Math.random() < 0.9) {
			enemy.hp -= this.att; 
		}
		else {
			enemy.hp = 0;
		}
	}

	
}

class Tank extends Unit {
	// 객체 생성되면, 자동으로 name은 "탱크", hp는 4000, att는 50
	public Tank() {
		super("탱크", 4000, 50);
	}
	// attack 오버라이드 
	// 1. 30% 확률로 상대의 hp 30% 감소
	// 2. 나머지 확률로 평타(일반 공격, 상대 hp를 50만큼 깎는다.)
	@Override
	public void attack(Unit enemy) {
	  if (Math.random() < 0.7) {
		  enemy.hp -= this.att; 
	  }
	  else {
		  enemy.hp *= 0.7;
    }
	}
	
}
public class Quiz02 {
	public static void main(String[] args) {
		Unit[] units = new Unit[2];
		for( int i=0; i < units.length; ++i ) {
			units[i] = Math.random() > 0.5 ? new Sniper() : new Tank();
		}
		System.out.println("1P : " + units[0].name );		
		System.out.println("2P : " + units[1].name );
		
		int count=1;
		while(true) {
			System.out.println("\n" + count + "차 공격");
			for(int i=0; i < units.length; ++i ) {
			System.out.println("1p(" + units[i].name +") 의 공격!");
			System.out.print("2p(" + units[(i+1)%2].name + ") 남은체력 : " + units[(i+1)%2].hp);
			units[i].attack(units[(i+1)%2]);
			System.out.println(" ==> " + units[(i+1)%2].hp);
			if( !units[(i+1)%2].getAlive()) {
				System.out.println((i+1)+"p(" + units[i].name +") WIN");
				return;
			}
			}
			++count;
		}
	}
}
```
#### 2. 탱크 vs 저격수 누가 더 쎌까? (그냥 궁금해서)
##### 1000번 시뮬 후 승률 출력
```java
  public class Quiz2_2 {
	public static void main(String[] args) {
		int tankWin=0;
		for(int j=1; j <= 1000; ++j) {
			Unit[] units = new Unit[2];
			for( int i=0; i < units.length; ++i ) {
				units[i] = Math.random() > 0.5 ? new Sniper() : new Tank();
			}
			System.out.println("======== < " + j + "차 시도 > ========");
			System.out.println("1P : " + units[0].name);		
			System.out.println("2P : " + units[1].name);
			
			int count=1;
			loop : while(true) {
				System.out.println("\n" + count + "차 공격");
				for(int i=0; i < units.length; ++i ) {
				System.out.println("1p(" + units[i].name +") 의 공격!");
				System.out.print("2p(" + units[(i+1)%2].name + ") 남은체력 : " + units[(i+1)%2].hp);
				units[i].attack(units[(i+1)%2]);
				System.out.println(" ==> " + units[(i+1)%2].hp);
				if( !units[(i+1)%2].getAlive()) {
					System.out.println((i+1)+"p(" + units[i].name +") WIN\n");
					if( units[i] instanceof Tank ) {
						++tankWin;
					}
					break loop;
				}
				}//for
				++count;
			}//while		
		}//for
		System.out.println("승률 : 탱크" + (tankWin/10.0) + "%, 저격수 " + (100 -(tankWin/10.0)) + "%");
	}//메인
  ```
