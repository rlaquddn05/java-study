#### callback조사하기
>  [ 콜백 (Callback) ]
>  	피호출자(Callee)가 호출자(Caller)를 다시 호출하는 것
>		비동기적(Asynchronous) 처리를 하기 위한 디자인 패턴의 종류
>  
>  비동기적 처리과정에서 caller가 호출시기를 알기 위해 callee를 지속적으로 모니터링 할 필요를 줄일 수 있다.
>  (homework1의 buy()에서도 무한루프를 통해 계속 occupancy를 체크하고 있었음)
> 
>  구현방법으로는 caller객체의 레퍼런스를 callee에게 피딩해주어 caller의 함수를 이용할 수 있게 하면 될 것으로 보인다.
>  
>  아래는 Homework1의 	buy()에서도 무한루프를 통해 지속적으로 occupancy를 체크하는 부분을 제거하고 VendingMachine의
>  sell함수의 마지막에 다시 buy()를 호출하는 명령을 추가해 보았다.
>  이러한 구조가 콜백구조의 예시인것 같다.

```java
package day25.homework;

class VendingMachine2 {
	boolean occupancy;
	String name;
	HumanThread2[] humanThreads;
	
	synchronized public void sell(String name, HumanThread2[] humanThreads) {
		this.occupancy = true;
		System.out.println(this.name + "에서 " + name + " 구매시작");
		try {
			Thread.sleep(2000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(this.name + "에서 " + name + " 구매완료!");
		this.occupancy = false;
		for(HumanThread2 ht : humanThreads ) {
			ht.buy(Homework02.vendingMachines);
		}
	}
}

class HumanThread2 extends Thread {
	int buyCount = 0;
	VendingMachine2[] vm;

	@Override
	public void run() {
		buy(vm);
	}

	public void buy(VendingMachine2[] vendingMachines) {
		for (VendingMachine2 vm : vendingMachines) {
			if (vm.occupancy == false && buyCount < 1) {
				++buyCount;
				vm.sell(this.getName(),Homework02.humanThreads);
			}
		}
	}
}

public class Homework02 {
	static VendingMachine2[] vendingMachines = new VendingMachine2[2];
	static HumanThread2[] humanThreads = new HumanThread2[10];
	
	public static void main(String[] args) {
		for (int i = 0; i < 2; ++i) {
			vendingMachines[i] = new VendingMachine2();
			vendingMachines[i].name = (i + 1) + "번 자판기";
		}

		for (int i = 0; i < 10; ++i) {
			humanThreads[i] = new HumanThread2();
			humanThreads[i].setName((i + 1) + "번 사람");
			humanThreads[i].vm = vendingMachines;
			humanThreads[i].start();
		}
		System.out.println("사람들 전부 자판기 이용 시작!");
	}
}
```
