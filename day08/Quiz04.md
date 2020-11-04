### day08.Quiz04
> 1. Scanner를 사용하여 6개의 데이터를 입력 받고, 이들을 nums 배열에 저장
> 2. 입력 받은 값 중, 20 이상 100 이하인 원소만 출력
> 3. 입력 받은 값 중, 최댓값과 최솟값을 출력
> 4. 오름차순(작은->큰)으로 정렬하여 모든 원소를 출력  ==> 버블 정렬 알고리즘 검색해서 ... 


```java
package day08.quiz;

import java.util.Scanner;

public class Quiz04 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		// 숫자6개 입력받아 nums배열에 저장
		int nums[] = new int[6];
		for (int i = 0; i < nums.length; ++i) {
			System.out.print((i + 1) + "번째 수를 입력하세요 : ");
			nums[i] = sc.nextInt();
		}
		sc.close();

		// 입력받은 값 중 20 이상 100 이하인 원소만 출력
		System.out.print("입력한 수 중 20 이상 100 이하인 수 : ");
		for (int d : nums) {
			if (d >= 20 && d <= 100) {
				System.out.print(d + " ");
			}
		}

		// 입력받은 값 중 최대값, 최소값 출력
		int max = nums[0];
		int min = nums[0];
		for (int i = 1; i < nums.length; ++i) { // i=0 아닌 1부터 시작하면 연산횟수 감소
			if (nums[i] >= max) {
				max = nums[i];
			}
			if (nums[i] <= min) {
				min = nums[i];
			}
		}
		System.out.println("\n최대값 : " + max + "\n최소값 : " + min);

		// 버블 정렬 알고리즘을 활용하여 오름차순으로 정리하여 출력
		int temp;
		int i, j;
		for (i = (nums.length - 1); i > 1; --i) {
			for (j = 0; j < i; ++j) {
				if (nums[j] > nums[j + 1]) {
					temp = nums[j];
					nums[j] = nums[j + 1];
					nums[j + 1] = temp;
				}
			}
		}
		for (int d : nums) {
			System.out.print(d + " ");
		}

	}
}
```
