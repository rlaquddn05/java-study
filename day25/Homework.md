### day25.Homework
> - run()에서 vendingMachine[]를 읽어들이고 싶은데 void메소드를 오버라이드 해야하니 buy()를 만들어 run()은 buy()만 실행하였다(불안...)   
> - VendingMachine, HumanThread의 하위 class를 만들면 1. 음료 뽑는 시간이 다른 여러 자판기, 2. 각 사람이 사야하는 음료의 갯수가 다른 경우 등으로 응용 가능할 것 같다
> - 게터 세터 일단 배제(문제를 맞게 이해했는지부터 )


##### 문제 : 동기 (synchronized) 사용하여 자판기 구현하기    
> 	1) 자판기는 2개가 있다.   
> 	2) 사람쓰레드는 10개가 있다.   
> 	3) 자판기에서 음료를 뽑는 시간은 3초다.   
> 	4) 사람쓰레드는 1번 자판기를 우선적으로 선택하되    
> 	자판기가 사용중이라면 2번 자판기를 사용한다.   
> 	2번 자판기도 사용중이라면 1번 자판기로 가서 기다린다.   
> 	+ 1, 2 번 자판기 중 먼저 사용가능한 자판기를 선택하여 사용한다.   


```java
package day25.homework;

class VendingMachine {
	boolean occupancy;
	String name;

	synchronized public void sell(String name) { 
		this.occupancy = true;
		System.out.println(this.name + "에서 " + name + " 구매시작");
		try {
			Thread.sleep(2000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(this.name + "에서 " + name + " 구매완료!");
		this.occupancy = false;
	}
}

class HumanThread extends Thread {
	int buyCount = 0;

	@Override
	public void run() { 
		buy(Homework.vendingMachines);
	}

	public void buy(VendingMachine[] vendingMachines) {
		while (buyCount < 1) {
			for (VendingMachine vm : vendingMachines) {
				if (vm.occupancy == false && buyCount < 1) {
					++buyCount;
					vm.sell(this.getName());
				}
			}
		}
	}
}

public class Homework {
	static VendingMachine[] vendingMachines = new VendingMachine[2]; // void 메소드인 run()에서 배열을 읽어들이기 위해 static선언
	static HumanThread[] humanThreads = new HumanThread[10]; // 이건 그냥 보기 좋으라고 같이 static
  
	Homework() { // 
		for (int i = 0; i < 2; ++i) {
			vendingMachines[i] = new VendingMachine();
			vendingMachines[i].name = (i + 1) + "번 자판기";
		}

		for (int i = 0; i < 10; ++i) {
			humanThreads[i] = new HumanThread();
			humanThreads[i].setName((i + 1) + "번 사람");
			humanThreads[i].start();
		}
		System.out.println("사람들 전부 자판기 이용 시작!");
	}

	public static void main(String[] args) {
		new Homework();
	}
}
```
##### 피드백 : 자판기를 static 말고 HumanThread에 전달하는 형태로
> HumanThread에 VendingMachine[] vm 필드를 만들고 메인에서 필드에 vendingMachines의 레퍼런스를 저장해주는 방식으로 
```java
package day25.homework;

class VendingMachine {
	boolean occupancy;
	String name;

	synchronized public void sell(String name) { 
		this.occupancy = true;
		System.out.println(this.name + "에서 " + name + " 구매시작");
		try {
			Thread.sleep(2000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(this.name + "에서 " + name + " 구매완료!");
		this.occupancy = false;
	}
}

class HumanThread extends Thread {
	int buyCount = 0;
	VendingMachine[] vm;
	
	@Override
	public void run() { 
		buy(vm);
	}

	public void buy(VendingMachine[] vendingMachines) {
		while (buyCount < 1) {
			for (VendingMachine vm : vendingMachines) {
				if (vm.occupancy == false && buyCount < 1) {
					++buyCount;
					vm.sell(this.getName());
				}
			}
		}
	}
}

public class Homework {
	public static void main(String[] args) {
		VendingMachine[] vendingMachines = new VendingMachine[2]; // void 메소드인 run()에서 배열을 읽어들이기 위해 static선언
		HumanThread[] humanThreads = new HumanThread[10]; // 이건 그냥 보기 좋으라고 같이 static
		for (int i = 0; i < 2; ++i) {
			vendingMachines[i] = new VendingMachine();
			vendingMachines[i].name = (i + 1) + "번 자판기";
		}

		for (int i = 0; i < 10; ++i) {
			humanThreads[i] = new HumanThread();
			humanThreads[i].setName((i + 1) + "번 사람");
			humanThreads[i].vm = vendingMachines;
			humanThreads[i].start();
		}
		System.out.println("사람들 전부 자판기 이용 시작!");		
	}
}
```
