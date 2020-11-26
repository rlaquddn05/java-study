### day24.homework
> 19일차 숙제에 사용자 정의 예외 붙이기
> Patternexception 추가, 아이디 비밀번호를 각각 틀렸을때 다른 메시지 출력

```java
package day24.homework;

import java.util.Scanner;
import java.util.regex.Pattern;

interface Rule {
	public static final String MAIL_PATTERN = "^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$";
	public static final String PW_PATTERN = "^(?=.*\\d)(?=.*[~`!@#$%\\^&*()-])(?=.*[a-z])(?=.*[A-Z]).{4,20}$";
}

@SuppressWarnings("serial")
class PatternException extends Throwable {
	public PatternException() {
		super("올바른 형식에 맞추어야 합니다");
	}

	public PatternException(String message) {
		super(message);
	}
}

public class Homework01 implements Rule {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		String eMail;
		String pw;
		String pw2;
		System.out.print("이메일을 입력하세요 : ");
		while (true) {
			try {
				eMail = sc.next().trim();
				if (!Pattern.matches(Rule.MAIL_PATTERN, eMail)) {
					throw new PatternException();
				}
				System.out.print("비밀번호를 입력하세요 : ");
				while (true) {
					try {
					pw = sc.next().trim();
					if (!Pattern.matches(Rule.PW_PATTERN, pw)) {
						throw new PatternException();
					}
					System.out.print("한번 더 입력하세요: ");
					pw2 = sc.next().trim();
					if (!pw.equals(pw2)) {
						System.out.print("두 비밀번호는 같아야 합니다.\n비밀번호를 다시 입력하세요 : ");
						continue;
					}
					} catch (PatternException e) {
						System.out.print("올바른 비밀번호 형식으로 다시 입력해주세요 : ");
						continue;
					}
					break;
				}
			} catch (PatternException e) {
				System.out.print("올바른 아이디 형식으로 다시 입력해주세요 : ");
				continue;
			}
			break;
		}
		sc.close();
		System.out.println("ID : " + eMail.split("@")[0]);
		System.out.println("PW : " + pw.replaceAll("(?<=..).", "*"));
		System.out.println("E-mail : " + eMail);
	}
}
```
