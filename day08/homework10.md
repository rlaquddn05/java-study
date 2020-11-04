### day08.homework10
> //호텔관리 프로그램 만들기    
> //step1) 사용자에게 호텔의 방 개수를 입력 받습니다.    
> //step2) 방개수와 동일한 크기의 배열을 생성합니다. (5개면 5칸짜리 배열 생성)    
> //  step3) 사용자 메뉴를 메시지로 보여주고 메뉴를 선택 받습니다.    
> //      < 메뉴 >    
> //      1. 체크인    
> //      2. 체크아웃    
> //      3. 현황 보기    
> //      0. 종료하기    
> //    
> //      1. 체크인    
> //          방 호수(1번부터 시작)를 입력 받습니다.    
> //          방이 이미 입실 중이면 "입실 중인 방은 체크인 하실 수 없습니다."를 출력하세요.    
> //          빈 방인 경우 "입실 완료!"를 출력하고 메뉴로 돌아갑니다.    
> //      2. 체크아웃    
> //          방 호수(1번부터 시작)를 입력 받습니다.    
> //          방이 빈 방이면 "빈 방은 체크아웃 하실 수 없습니다."를 출력하세요.    
> //          체크인 상태인 경우 "퇴실 완료!"를 출력하고 메뉴로 돌아갑니다.    
> //      3. '방호수 - 상태'를 출력합니다.    
> //          출력 예)    
> //              1호 : 빈 방    
> //              2호 : 입실 중    
> //              3호 : 입실 중    
> //              4호 : 빈 방    
> //              5호 : 빈 방    
> //      0. 종료    
> //          반복을 종료하고 '영업 종료' 를 출력합니다.    
> //    
> //  (힌트 : 사용자가 4호에 입실한다면 [3]번칸에 1을 저장하고 퇴실한다면 0을 저장합니다. 즉 투숙객이 있음은 1로 없으면 0으로 표시합니다.)    
> //    
> //  step4) 사용자가 메뉴에서 0을 입력할 때까지 (3) 과정을 진행합니다.    
```java
import java.util.Scanner;

public class homework10 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("호텔의 방 갯수를 입력하세요: ");
		int roomNo = sc.nextInt();
		int[] hotel = new int[roomNo];

		while (true) {
			System.out.print("==========\n1. 체크인\n" + "2. 체크아웃\n" + "3. 현황 보기\n" 
								+ "0. 종료하기\n==========\n원하시는 메뉴를 선택하세요: ");
			int input = sc.nextInt();

			switch (input) {
				case 1: {
					System.out.print("원하시는 방 호수를 입력하세요 (최대" + roomNo + ") : ");
					int input1 = sc.nextInt();

					if (hotel[input1 - 1] == 0) {
						hotel[input1 - 1] = 1;
						System.out.println("입실완료!");
					} 
					else {
						System.out.println("입실중인 방은 체크인 하실 수 없습니다.");
					}
					break;
				}

				case 2: {
					System.out.print("퇴실하시는 방 호수를 입력 해주세요 : ");
					int input2 = sc.nextInt();

					if (hotel[input2 - 1] == 1) {
						hotel[input2 - 1] = 0;
						System.out.println("퇴실완료!");
					} 
					else {
						System.out.println("빈 방은 체크아웃 하실 수 없습니다.");
					}
					break;
				}

				case 3: {
					for (int i = 0; i < roomNo; ++i) {
						System.out.print((i + 1) + "호: ");
						if (hotel[i] == 0) {
							System.out.println("빈 방");
						}
						else {
							System.out.println("입실 중");
						}
					}
					break;
				}	
				

				case 0: {
					sc.close();
					return;
				}
			}//switch(메뉴선택후)
		}//while(메뉴)
	}//메인
} //클래스
```
