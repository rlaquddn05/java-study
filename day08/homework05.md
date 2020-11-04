### day08.homework05
> 하-5 : 사용자에게 배열의 칸 개수를 입력 받고, 해당 정수의 크기만큼 String형 배열을 생성하고   
> 입력 : 3  ===> 결과 : [ null, null, null ]    
> 입력 : 5  ===> 결과 : [ null, null, null, null, null ]   
>   
> 사용자에게 입력받은 단어들을 순차적으로 배열에 저장하세요.    
```java
package day08.homework;

import java.util.Scanner;

public class homework05 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int num;
		while (true) { // 칸 수 입력받기(양수가 아닌 숫자 입력시 다시 입력받기)
			System.out.print("배열의 칸 갯수를 입력하세요 : ");
			num = sc.nextInt();
			if (num > 0) {
				break;
			} else
				System.out.println("올바른 칸 갯수를 입력하세요.");
		}
		sc.nextLine();	
	
		String[] sArray;
		sArray = new String[num];
		
		for(int i=0; i<sArray.length;++i) {
			System.out.print((i+1)+"번째 자료를 입력하세요 : ");
			sArray[i] = sc.nextLine();
		}
		sc.close();
		
		System.out.print("결과 : [ "); // sArray에 입력된 값 출력
		for (int i = 0; i < sArray.length; ++i) {
			if (i < (sArray.length - 1)) {
				System.out.print(sArray[i] + ", ");
				continue;
			}
			System.out.println(sArray[i] + " ]");
		}
	
	}
}
```
