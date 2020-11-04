### day08.homework11
> //로또생성기 만들기    
> //step1) 사용자에게 1 ~ 45 중 6개의 숫자를 입력 받습니다.        
> //step2) 컴퓨터는 로또 번호 6개를 생성합니다. 배열의 크기는 6이고 int형입니다.    
> //step3) 1 ~ 45 중 6개의 숫자를 배열에 담습니다. 중복된 원소가 있으면 안됩니다.    
> //step4) (구현 가능하다면) 오름차순 정렬을 합니다.    
> //step5) 배열 결과를 출력합니다.    
> //step6) 사용자가 몇 개의 번호를 맞췄는지 출력하세요.    
```java
package day08.homework;

import java.util.Scanner;

public class homework11 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		// step1 사용자의 숫자 입력받기, 중복 또는 45이상의 숫자 입력시 다시 입력
		int[] userNo = new int[6];
		for (int i = 0; i < 6; i++) {
			System.out.print((i + 1) + "째 번호를 입력하세요 : ");
			userNo[i] = sc.nextInt();
			for (int j = 0; j < i; j++) {
				if (userNo[j] == userNo[i]) { // 그 전까지 생성된 userNo[]들과 userNo[i]비교
					i--; // 같은숫자가 발견되면 i--하여 다시 생성
					System.out.println("같은 숫자는 입력하실 수 없습니다.");
				}
				if (userNo[i] > 45) {
					i--;
					System.out.println("1 ~ 45중의 숫자를 입력하세요.");
				}
			}
		}

		// step2 & step3 로또번호 생성, 중복숫자 발생시 다시 생성
		int[] lotto = new int[6];
		for (int i = 0; i < 6; i++) {
			lotto[i] = (int) (Math.random() * 45) + 1; // lotto[i]의 번호 생성
			for (int j = 0; j < i; j++) {
				if (lotto[j] == lotto[i]) { // 그 전까지 생성된 lotto[]들과 lotto[i]비교
					i--; // 같은숫자가 발견되면 i--하여 다시 생성
				}
			}
		}

		// step4 userNo 오름차순
		int i, j, temp;
		for (i = 5; i > 1; --i) {
			for (j = 0; j < i; ++j) {
				if (userNo[j] > userNo[j + 1]) {
					temp = userNo[j];
					userNo[j] = userNo[j + 1];
					userNo[j + 1] = temp;
				}
			}
		}

		// step4-2 lotto오름차순
		for (i = 5; i > 1; --i) {
			for (j = 0; j < i; ++j) {
				if (lotto[j] > lotto[j + 1]) {
					temp = lotto[j];
					lotto[j] = lotto[j + 1];
					lotto[j + 1] = temp;
				}
			}
		}

		// step5 userNo출력
		System.out.print("당신의 숫자 : [ ");
		for (i = 0; i < 6; ++i) {
			if (i < 5) {
				System.out.print(userNo[i] + ", ");
				continue;
			}
			System.out.println(userNo[i] + " ]");
		}

		// step5-2 lotto출력
		System.out.print("당 첨 번 호 : [ ");
		for (i = 0; i < 6; ++i) {
			if (i < 5) {
				System.out.print(lotto[i] + ", ");
				continue;
			}
			System.out.println(lotto[i] + " ]");
		}

		// step6 결과 출력
		int count = 0;
		for (i = 0; i < 6; ++i) {
			if (userNo[i] == lotto[i]) {
				count++;
			}
		}
		if(count>=4) {
		System.out.println("당신이 맞춘 숫자는 " + count + " 개 이며," + (8 - count) + "등 입니다!");
		}
		else System.out.println(count + "개 맞추셨습니다. 꽝!" );
	}
}
```
