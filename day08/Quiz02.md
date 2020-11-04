## day08.Quiz02

> double형 4칸짜리 배열을 생성하고    
> Scanner를 사용하여 각 원소를 입력 받음   
> 입력 후 모든 원소를 출력   
> a[0] = sc.nextDouble();   

```java
package day08.quiz;

import java.util.Scanner;

public class Quiz02 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		double[] arr;
		arr = new double[4];

		for (int i = 0; i < arr.length; ++i) {
			System.out.print((i + 1) + "번째 원소: ");
			arr[i] = sc.nextDouble();
		}
		sc.close();

		for (double d : arr) {
			System.out.print(d + " ");
		}

	}
}
```
