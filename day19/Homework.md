### day19.Homework01
> 1. 사용자가 -1을 입력할 때까지 문자열을 입력 받고   
>     1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.   
>     2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.   
>     3) 단어의 개수를 출력하세요.   

```java
package day19.homework;

import java.util.Scanner;

//1. 사용자가 -1을 입력할 때까지 문자열을 입력 받고
//1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.
//2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.
//3) 단어의 개수를 출력하세요.
public class Homework01 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("문자열들을 원하시는 만큼 입력하세요.\n-1 입력시 종료합니다.");
		String total="";

		int aCount = 0;
		int charCount = 0;
		int wordCount = 0;
		
		int idx = 1;
		while (true) {
			System.out.print(idx + "번째 문자열을 입력하세요 : ");
			String input = sc.nextLine().trim();
			if( input.equals("-1") ) {
				break;
			}
			total += (" " + input);
			++idx;
		}
		sc.close();
		
		
		for (int i = 0; i < total.toCharArray().length; ++i) {
			if (total.toCharArray()[i] == 'a') {
				++aCount;
			}
		}
		charCount += total.replaceAll("[ \t\n\\x0B\f\r]", "").length();
		wordCount += total.split(" ").length;
				
		System.out.println("a를 입력한 횟수 : " + aCount);
		System.out.println("비출력문자를 제외한 총 문자 수 : " + charCount);
		System.out.println("단어의 총 갯수 : " + wordCount);

	}
}

```
### day19.Homework02
> 2. 회원가입과정은 다음과 같습니다.   
> 	1) 이메일을 입력 받는다.   
> 	2) 비밀번호를 2번 입력받는다.   
> 	   
>    이때 다음 조건에 충족하면 저장, 그렇지 않으면 해당 항목을 재입력 받으세요   
>  	1) 이메일 조건      
> 		- @ 를 포함하여야 한다.   
> 		- com, co.kr, net 중 하나로 끝나야 한다   
> 		- 메일서버(naver, gmail, hanmail 등) 이름을 포함해야 한다.   
> 		- 아이디가 있어야 한다.   
> 		- 공백이 있다면 제거한다.   
> 		   
> 	2) 비밀번호 조건   
> 		- 4자 이상 20자 이하여야 한다.   
> 		- (선택사항) 특수기호, 숫자, 대소문자가 최소 1개씩 모두 있어야 한다. (String 클래스의 matches()사용)   
> 		- 두 비밀번호가 동일해야 한다.   
>    
>   모두 정상적인 입력을 받았다면 사용자의 id, 패스워드, 이메일을 출력하세요.   
> 	1) id 는 이메일의 @ 앞 부분을 추출합니다.   
> 	2) 비밀번호는 앞 두 글자만 출력하고 나머지는 '*'로 대체합니다.   
> 		예) pika1234 ==> pi******   
> 	3) 이메일은 모두 출력합니다.   

```java
package day19.homework;

import java.util.Scanner;
import java.util.regex.Pattern;

interface Rule {
	public static final String MAIL_PATTERN = "^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$";
	public static final String PW_PATTERN = "^(?=.*\\d)(?=.*[~`!@#$%\\^&*()-])(?=.*[a-z])(?=.*[A-Z]).{4,20}$";
}

public class Homework02 implements Rule {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		String eMail;
		String pw;
		String pw2;
		System.out.print("이메일을 입력하세요 : ");
		while (true) {
			eMail = sc.next().trim();
			if (!Pattern.matches(Rule.MAIL_PATTERN, eMail)) {
				System.out.print("올바른 이메일 형식이 아닙니다.\n이메일을 다시 입력하세요 : ");
			} else {
				System.out.print("비밀번호를 입력하세요 : ");
				while (true) {
					pw = sc.next().trim();
					if (!Pattern.matches(Rule.PW_PATTERN, pw)) {
						System.out.print("올바른 비밀번호 형식이 아닙니다.\n비밀번호를 다시 입력하세요 : ");
					} else {
						System.out.print("한번 더 입력하세요: ");
						pw2 = sc.next().trim();
						if (!pw.equals(pw2)) {
							System.out.print("두 비밀번호는 같아야 합니다.\n비밀번호를 다시 입력하세요 : ");
						} else {
							sc.close();
							System.out.println("ID : " + eMail.split("@")[0]);
							String showAsterisk = "";
							for (int i = 1; i <= pw.length() - 2; ++i) {
								showAsterisk += "*";
							}
							System.out.println("PW : " + pw.charAt(0) + pw.charAt(1) + showAsterisk);
							System.out.println("E-mail : " + eMail);
							return;
						}
					}
				}
			}
		}
	}
}
```


