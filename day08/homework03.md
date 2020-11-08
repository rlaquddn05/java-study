### day08.homework03
> 하-3 : 사용자에게 배열의 칸 개수를 입력 받고, 해당 정수의 크기만큼 정수형 배열을 생성하세요.   
>		입력 : 3  ===> 결과 : [ 0, 0, 0 ]    
>		입력 : 5  ===> 결과 : [ 0, 0, 0, 0, 0 ]    
```java
package day08.homework;

import java.util.Scanner;


public class homework03 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int num = 0;
		while (true) { 
			System.out.print("배열의 칸 갯수를 입력하세요 : ");
			num = sc.nextInt();
			if (num > 0) {
				break;
			} else
				System.out.println("올바른 칸 갯수를 입력하세요.");
		}
		sc.close();

		int[] array;
		array = new int[num];
		
		System.out.print("결과 : [ ");
		for (int i = 0; i < array.length; ++i) {
			if(i<(array.length-1)) {
				System.out.print(array[i] + ", ");
				continue;
			}
			System.out.println(array[i]+" ]");
		}
		
		// String.join을 사용하는 경우(?)
		String[] sArray;
		sArray = new String[num];
		for (int i = 0; i < array.length; ++i) {
			sArray[i] = Integer.toString(array[i]);
		}
		System.out.println( "결과 : [ " + String.join(", ", sArray ) + " ]"  );
	}
}
```
