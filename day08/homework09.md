### day08.homework09
> //대학생 새내기들의 90%는 자신이 반에서 평균은 넘는다고 생각한다. 당신은 그들에게 슬픈 진실을 알려줘야 한다.   
> //   
> //입력   
> //첫째 줄에는 테스트 케이스의 개수 C가 주어진다.   
> //   
> //둘째 줄부터 각 테스트 케이스마다 학생의 수 N(1 ≤ N ≤ 1000, N은 정수)이 첫 수로 주어지고, 이어서 N명의 점수가 주어진다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.   
> //   
> //출력   
> //각 케이스마다 한 줄씩 평균을 넘는 학생들의 비율을 반올림하여 소수점 셋째 자리까지 출력한다.   
```java
package day08.homework;

import java.text.DecimalFormat;
import java.util.Scanner;

public class homework09 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		DecimalFormat df = new DecimalFormat(".000");
		
		System.out.print("테스트 케이스의 개수를 입력하세요 : ");
		int c = sc.nextInt();
		int n;
		String [] percentage = new String[c]; 
				
		for(int i=0; i<c; ++i) {
			System.out.print("\n==="+(i+1)+"째 테스트 케이스 정보를 입력하세요===\n"
					+ (i+1)+ "째 테스트 케이스의 학생 숫자를 입력하세요: ");
			n = sc.nextInt();
			int [] score = new int[n];
			int avg=0;
			int count=0;
			
			
			for(int j=0; j<n; ++j) {
				System.out.print("학생"+(j+1)+"의 점수를 입력하세요: ");
				score[j] = sc.nextInt();
				avg += score[j];
			}
			
			avg /= (double)n;
			
			for(int j=0; j<n; ++j) {
				if(score[j]>avg) {
					++count;
				}
			}
			
			percentage[i] = df.format((double)count/n*100);
			
		}
		
		System.out.println("\n================결과================");
		for(int i=0; i<c; ++i) {
		System.out.println((i+1)+"째 케이스의 평균을 넘는 학생의 비율은 : " + percentage[i]+"%");
		sc.close();
		}
	}
}
```
