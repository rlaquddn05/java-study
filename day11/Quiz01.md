### FunctionFactory 실행 메인메소드
```java
package day11.quiz;

public class Quiz01 {
	public static void main(String[] args) {
		FunctionFactory myFac = new FunctionFactory();
		
		String s1 = myFac.strGugudan(5);
		System.out.println(s1);
		
		myFac.printGugudan(5);
		
		System.out.println(myFac.getAverage(90, 80, 100));
		
		System.out.println(myFac.getRandomPokemon());
		
		int[] b = {10, 2, 4, 6, 2, 100, 15};
		System.out.println(myFac.getMax(b));
	}
}
```
