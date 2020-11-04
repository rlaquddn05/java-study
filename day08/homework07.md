### day08.homework07
> //dates 배열은 다음과 같이 1~12월의 최대 일자가 들어있습니다.    
> //==> int[] dates = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};     
> //    
> //1) dates 배열을 활용하여 1/1일부터 사용자에게 입력 받은 월/일 까지 며칠이 소요되는지 출력하세요.    
> //  단, 사용자에게 해는 따로 입력받지 않기때문에 윤년은 없다고 가정합니다.    
> //    
> //	예) 월 : 12   일 : 31  ==> 364일 소요!    
> //	    월 : 4    일 : 12   ==> 101일    
> //	원리) 4/12 의 결과를 계산하려면    
> //	    1 / 1 ~ 1 / 31  => 31 (dates[0])     
> //	    2 / 1 ~ 2 / 28  => 28 (dates[1])    
> //	    3 / 1 ~ 3 / 31  => 31 (dates[2])    
> //   	4 / 1 ~ 4 / 12  => 12 (사용자가 입력한 일)    
> //	 => 31 + 28 + 31 + 12 - 1 = 101일     
> //    
> //2) 시작월/일과 목표 월/일 을 각각 입력 받고 d-day 계산기를 만드세요.    
> //  단, year는 입력받지 않기때문에 d-day의 최댓값은 364일로 가정합니다.    
> //  예) 시작 : 9/26  목표 : 11/23  ==> 결과 : d-day 58 !!!    
> //      시작 : 1/1 목표 : 12/31  ==> 결과 : d-day 364 !!!    
> //      시작 : 12/31 목표 : 1/1  ==> 결과 : d-day 1 !!!    
> //      시작 : 4/12 목표 : 4/11  ==> 결과 : d-day 364 !!!    
> //  원리)    
> //	start : 1/1 ~ 시작 월/일까지 며칠이 소요되는지 계산합니다.     
> //	end : 1/1 ~ 목표 월/일까지 며칠이 소요되는지 계산합니다.     
> //	end-start 를 합니다.     
> //	이때 음수가 나온다면 목표일이 시작일보다 앞서있다는 의미입니다. (즉 목표일이 이듬해)    
> //	이 경우 +365를 하면 됩니다.    
```java
package day08.homework;

import java.util.Scanner;

public class homework07 {
	public static void main(String[] args) {
		int[] dates = { 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
		Scanner sc = new Scanner(System.in);

//		1) 입력받은 월/일 까지 몇일이 소요되는지 구하기
		System.out.print("날짜를 입력하세요(월/일): ");
		String input = sc.nextLine();
		int inDate[] = { 0, 0 };
		inDate[0] = Integer.parseInt(input.split("/")[0]);
		inDate[1] = Integer.parseInt(input.split("/")[1]);

		int dday0 = 0;
		for (int i = 0; i <= inDate[0] - 2; ++i) {
			dday0 += dates[i];
		}
		dday0 += inDate[1];
		System.out.println("1월 1일 부터 지난 날짜 : " + dday0);

//		2) 시작날짜, 끝날짜 입력받고 dday구하기
		System.out.print("\n시작 날짜를 입력하세요(월/일): ");
		String start = sc.nextLine();
		int sDate[] = { 0, 0 };
		sDate[0] = Integer.parseInt(start.split("/")[0]);
		sDate[1] = Integer.parseInt(start.split("/")[1]);

		int sdday = 0;
		for (int i = 0; i <= sDate[0] - 2; ++i) {
			sdday += dates[i];
		}
		sdday += sDate[1]; // 1월1일부터 시작날 까지의 dday

		System.out.print("끝 날짜를 입력하세요(월/일): ");
		String end = sc.nextLine();
		sc.close();
		int eDate[] = { 0, 0 };
		eDate[0] = Integer.parseInt(end.split("/")[0]);
		eDate[1] = Integer.parseInt(end.split("/")[1]);
		
		
		int edday = 0;
		for (int i = 0; i <= eDate[0] - 2; ++i) {
			edday += dates[i];
		}
		edday += eDate[1]; // 1월1일부터 끝날 까지의 dday

		int dday = edday - sdday;
		if (dday > 0) {
			System.out.println("dday는 " + dday + "일 입니다.");
		} else if (dday < 0) {
			System.out.println("dday는 " + (dday + 365) + "일 입니다.");
		} else
			System.out.println("당일입니다.");

	}
}
```
