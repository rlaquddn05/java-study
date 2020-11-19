####day19.Homework01
> 1. 사용자가 -1을 입력할 때까지 문자열을 입력 받고   
>     1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.   
>     2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.   
>     3) 단어의 개수를 출력하세요.   

```java
public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("문자열들을 원하시는 만큼 입력하세요.(최대 100개)\n-1 입력시 종료합니다.");
		String[] inputs = new String[100];

		int aCount = 0;
		int charCount = 0;
		int wordCount = 0;
		
		int idx = 0;
		while (idx < 100) {
			System.out.print(idx + 1 + "번째 문자열을 입력하세요 : ");
			inputs[idx] = sc.nextLine();
			inputs[idx] = inputs[idx].trim();
			
			if( inputs[idx].equals("-1") ) {
				break;
			}
			
			for (int i = 0; i < inputs[idx].toCharArray().length; ++i) {
				if (inputs[idx].toCharArray()[i] == 'a') {
					++aCount;
				}
			}
			charCount += inputs[idx].replace(" ", "").length();
			wordCount += inputs[idx].split(" ").length;
			++idx;
		}
		sc.close();
		System.out.println("a를 입력한 횟수 : " + aCount);
		System.out.println("비출력문자를 제외한 총 문자 수 : " + charCount);
		System.out.println("단어의 총 갯수 : " + wordCount);

	}
}
```
