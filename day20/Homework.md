### Homework01
> 1. 디데이 계산기를 만드세요.    
>   시작년월일 입력 --> 목표 년월일 입력 ---> D-Day XX!!!     
```java
package day20.homework;

import java.util.Calendar;
import java.util.Scanner;

public class Homework01 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("시작일을 입력하세요(년/월/일) : ");
		String[] sStartDay = sc.next().trim().split("/");
		int[] startDay = new int[3];
		for (int i = 0; i < sStartDay.length; ++i) {
			startDay[i] = Integer.parseInt(sStartDay[i]);
		}
		System.out.print("종료일을 입력하세요(년/월/일) : ");
		String[] sEndDay = sc.next().trim().split("/");
		int[] endDay = new int[3];
		for (int i = 0; i < sEndDay.length; ++i) {
			endDay[i] = Integer.parseInt(sEndDay[i]);
		}
		sc.close();

		Calendar start = Calendar.getInstance();
		Calendar end = Calendar.getInstance();
		start.set(startDay[0], startDay[1] - 1, startDay[2]);
		end.set(endDay[0], endDay[1] - 1, endDay[2]);

		long dday = (end.getTimeInMillis() - start.getTimeInMillis()) / (60 * 60 * 24 * 1000);
		System.out.println();

		if (dday < 0) {
			System.out.println("시작일이 종료일보다 빨라야 합니다.");
		}
		System.out.println("D-day : " + dday);
	}
}
```

### Homework02
> 2. 년, 월을 입력 받고 해당 월을 달력형태로 출력하세요. (토요일마다 줄바꿈이 일어나도록)
```java
package day20.homework;

import java.util.Calendar;
import java.util.Scanner;

//2. 년, 월을 입력 받고 해당 월을 달력형태로 출력하세요. (토요일마다 줄바꿈이 일어나도록)
//2020 10
//일	월	화	수	목	금	토
//				1	2	3
//4	5	6	7	8	9	10
//11	12	13	14	15	16	17
//18	19	20	21	22	23	24
//25	26	27	28	29	30	31 

public class Homework02 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("년도를 입력하세요 : ");
		int year = sc.nextInt();
		System.out.print("월을 입력하세요 : ");
		int month = sc.nextInt();
		sc.close();

		String[][] body = new String[6][7];
		String[] line2 = { "일 ", "월 ", "화 ", "수 ", "목 ", "금 ", "토 " };
		Calendar cal = Calendar.getInstance();

		cal.set(Calendar.YEAR, year);
		cal.set(Calendar.MONTH, month - 1);
		cal.set(Calendar.DATE, 1);

		int startDay = cal.get(Calendar.DAY_OF_WEEK); // 1일이 무슨요일인지?
		int endDate = cal.getActualMaximum(Calendar.DATE); // 몇일로 끝나는지?

//body채우기
		int row = 0;
		int input = 1;
		for (int i = 1; input <= endDate; i++) { // i : body의 칸번호, input : 입력날짜, i=startDay부터 입력
		if (i < startDay) // 1일 보다 앞에는 공백2개씩
				body[row][i - 1] = "  ";
			else {
				body[row][(i - 1) % 7] = Integer.toString(input);
				if(input < 10) // 1자리 숫자와 2자리 숫자의 크기 다르므로 맞추어 준다
					body[row][(i - 1) % 7] += " ";
				++input;

				// 줄바꿈
				if (i % 7 == 0)
					row++;
			}
		}

//달력 
		System.out.println(year + "년" + month + "월");

		for (int i = 0; i < 7; ++i) {
			System.out.print(line2[i] + "  ");
		}
		System.out.println("");

		for (int i = 0; i <= 5; i++) {
			for (int j = 0; j <= 6; j++) {
				if (body[i][j] == null) {
					return;
				}
				System.out.print(body[i][j] + " ");
				if (j == 6) {
					System.out.println("\n");
				}
			}
		}

	}
}
```
