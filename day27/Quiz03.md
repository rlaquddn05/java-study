### Quiz03
```java
package day27.quiz;

import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;

import javax.swing.JOptionPane;

/*
 * Quiz01
 * 	-> 2단.txt ~ 9단.txt 구구단 텍스트 파일 생성
 * 
 * Quiz02
 *  -> 사용자에게 '단'을 입력 받아 해당 구구단 txt 파일을 열고, 
 *     그 내용을 jop으로 출력 
 * 
 * Quiz03 
 * 	-> 사용자에게 exit를 입력 받을 때까지 모든 문자열을 jop으로 입력 받고 
 *     exit를 입력 하면 YYYYMMdd_HHmmss.txt 형식으로 log 파일을 생성하여
 *     사용자가 입력한 모든 문자열 저장
 */
public class Quiz03 {
	public static void main(String[] args) {
		SimpleDateFormat sdf = new SimpleDateFormat("YYYYMMdd_HHmmss");
		String name = sdf.format(System.currentTimeMillis()) + ".txt";
		FileWriter writer = null;
		try {
			writer = new FileWriter(name);
			while (true) {
				String input = JOptionPane.showInputDialog("아무 문자열");
				if (input.contains("exit") && input.trim().length() == 4) {
					input = input.trim();
				}
				switch (input) {
				case "exit": {
					return;
				}
				default: {
					writer.write(input + "\n");
				}
				}
			}

		} catch (IOException e) {
			e.printStackTrace();
		} catch (NullPointerException e) {
			JOptionPane.showMessageDialog(null, "취소하셨습니다");
		} finally {
			try {
				if (null != writer)
					writer.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
}
```
