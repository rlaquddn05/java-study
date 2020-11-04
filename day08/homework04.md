### day08.homework04
> 하-4 : (3)번에서 생성된 배열에 다음 기능을 추가하세요.   
>	ㄱ. 0 ~ n-1 까지의 숫자를 배열에 순서대로 저장하세요.   
>		입력 : 3  ===> 결과 : [0, 1, 2]   
>		입력 : 5  ===> 결과 : [0, 1, 2, 3, 4]   
>	ㄴ. 배열의 가장 마지막 원소부터 0번 원소까지 역순으로 출력하세요.   
>	ㄷ. for문을 사용하여 배열에 저장된 실제 원소들을 역순으로 재배치 하세요. (난이도 중)   
>	    sysout(배열[0]); // 3   
>	    sysout(배열[1]); // 2   
>	    sysout(배열[2]); // 1   
>	    sysout(배열[3]); // 0   
>	   (for문을 쓰되 for문의 실행 횟수가 n/2이 되도록하세요.    
>        (5칸 배열이면 2회만에, 10칸 배열이면 5회만에 for문이 종료되도록))   
```java
package day08.homework;

import java.util.Scanner;

public class homework04 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int num = 0;
		while (true) { // 칸 수 입력받기(양수가 아닌 숫자 입력시 다시 입력받기)
			System.out.print("배열의 칸 갯수를 입력하세요 : ");
			num = sc.nextInt();
			if (num > 0) {
				break;
			} else
				System.out.println("올바른 칸 갯수를 입력하세요.");
		}
		sc.close();

		int[] array; // 배열 array 생성 후 숫자 저장 
		array = new int[num];
		for (int i = 0; i < array.length; ++i) {
			array[i] = i;
		}

		System.out.print("결과 : [ "); // array에 입력된 값 출력
		for (int i = 0; i < array.length; ++i) {
			if (i < (array.length - 1)) {
				System.out.print(array[i] + ", ");
				continue;
			}
			System.out.println(array[i] + " ]");
		}

		System.out.print("역순 : [ "); // array에 입력된 값을 역순으로 출력
		for (int i = array.length - 1; i >= 0; --i) {
			if (i > 0) {
				System.out.print(array[i] + ", ");
				continue;
			}
			System.out.println(array[i] + " ]");
		}

		int temp; // array에 입력되어 있는 값을 실제로 바꾸고 그 결과 출력
		for (int i = 0; i < (array.length / 2); i++) {
			temp = array[i];
			array[i] = array[array.length - 1 - i];
			array[array.length - 1 - i] = temp;
		}

		System.out.print("실제역순 : [ ");
		for (int i = 0; i < array.length; ++i) {
			if (i < (array.length - 1)) {
				System.out.print(array[i] + ", ");
				continue;
			}
			System.out.println(array[i] + " ]");
		}

	}
}
```
