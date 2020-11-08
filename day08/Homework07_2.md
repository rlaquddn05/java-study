### day08.Homework07_2
> Homework07 피드백 결과 :    
> sDate[0] = Integer.parseInt(start.split("/")[0]);   
>	sDate[1] = Integer.parseInt(start.split("/")[1]);   
>  의 split함수가 비용이 크므로 1회만 사용하는것이 바람직하다.   
>     
>  String[] 변수로 split을 받고 그 뒤 정수 파싱을 두번 수행.   
>     
>  람다를 사용하는것도 좋다.   
    
```java
package day08.homework;

import java.util.Scanner;

public class Homework07_2 {
//	static int[] cutdate(String s, int[] a) {
//		String t [] = new String[2];
//		t = s.split("/");
//		a[0] = Integer.parseInt(t[0]);
//		a[1] = Integer.parseInt(t[1]);
//		return a;
//	}
		
	static void cutdate2(String s, int[] a) {
		String t [] = new String[2];
		t = s.split("/");
		a[0] = Integer.parseInt(t[0]);
		a[1] = Integer.parseInt(t[1]);
	}
	
	public static void main(String[] args) {
		System.out.print("날짜를 입력하세요(월/일): ");
		Scanner sc = new Scanner(System.in);
		String input = sc.nextLine();
		sc.close();
		
//		int[] cut = new int[2];
//		System.out.println(cutdate(input, cut)[0]);
//		System.out.println(cutdate(input, cut)[1]);
		
		int[] cut = new int[2];
		cutdate2(input, cut);
		System.out.println(	cut[0] );
		System.out.println(	cut[1] );
		
		/*
		 * "/"을 기준으로 날짜를 월,일로 나누는 메소드 작성
		 * 1. 이걸 람다식으로 바꾸어 적용하는 법을 모르겠습니다...   
		 * 2. 람다식으로 세번쓰는것보다 그냥 메소드를 쓰는 것이 좋지 않나...
		 * 
		 */
	}
}
```
