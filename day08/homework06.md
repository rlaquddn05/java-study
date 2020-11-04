## day08.homework06
> "OOXXOXXOOO"와 같은 OX퀴즈의 결과가 있다. O는 문제를 맞은 것이고, X는 문제를 틀린 것이다.    
> 문제를 맞은 경우 그 문제의 점수는 그 문제까지 연속된 O의 개수가 된다. 예를 들어, 10번 문제의 점수는 3이 된다.   
> "OOXXOXXOOO"의 점수는 1+2+0+0+1+0+0+1+2+3 = 10점이다.   
> OX퀴즈의 결과가 주어졌을 때, 점수를 구하는 프로그램을 작성하시오.   
```java
package day08.homework;

import java.util.Scanner;

public class homework06 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("테스트 케이스의 갯수 입력 : ");
		int testnum = sc.nextInt();
		sc.nextLine();

		String[] result = new String[testnum]; // 테스트 갯수 입력받아 동일한 수의 원소를 가지는 배열 생성
		int[] score = new int[testnum]; // 점수를 입력할 배열 생성
		for (int i = 0; i < testnum; ++i) {
			System.out.print((i+1)+"번째 테스트 결과 입력 : ");
			result[i] = sc.nextLine(); // 각각의 테스트 결과 입력받기
			String[] onlyO = result[i].split("X"); // 입력받은 테스트 결과 잘라서 새로운 배열에 넣기
			for (String s : onlyO) {
				score[i] += s.length() * (s.length() + 1) / 2; // O의 갯수에 따라 점수 더하기
			}
		}
		
		System.out.println("====== 점수 ======");
		for (int i = 0; i < score.length; ++i) {
			System.out.println((i+1)+"번째 테스트 결과 : " + score[i] + "점" );
		}
		sc.close();
	}
}
```
