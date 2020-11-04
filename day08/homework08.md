### day08.homework08
> //"김", "이", "박", "최", "한" 등의 대한민국 성씨를 저장할 배열을 만들고, 성씨들을 저장하세요.    
> //"피카츄", "라이츄", "파이리", "꼬부기", "버터풀", "야도란", "피죤투" 를 저장할 배열을 만들고 이름들을 저장하세요.    
> //1) 총 10개의 성+이름 조합을 출력하세요. ( Math.random()을 사용하며, 중복 조합을 허용합니다)    
> //2) 조합가능한 모든 이름을 출력하세요.    
```java
package day08.homework;

public class homework08 {
	public static void main(String[] args) {
		String[] lName = { "김", "이", "박", "최", "한" };
		String[] fName = { "피카츄", "라이츄", "파이리", "버터풀", "야도란", "피죤투" };

//		1) 랜덤하게 10개 이름 출력
		System.out.println("===랜덤한 10개 이름 출력===");
		for (int i = 1; i <= 10; ++i) {
			int rand = (int) (Math.random() * 5);
			int rand2 = (int) (Math.random() * 6);
			System.out.println(i + ". " + lName[rand] + fName[rand2]);
		}

//		2) 가능한 모든 이름 출력
		System.out.println("\n===가능한 모든 이름 출력===");
		int no = 0;
		for (int i = 0; i < 5; ++i) {
			for (int j = 0; j < 6; ++j) {
				no++;
				System.out.println(no + ". " + lName[i] + fName[j]);
			}
		}

	}
}
```
