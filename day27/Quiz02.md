```java
package day27.quiz;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;

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
public class Quiz02 {
	public static void main(String[] args) {
		Scanner sc = null;
		FileReader reader = null;
		try {
		int dan = Integer.parseInt(JOptionPane.showInputDialog("몇단을 출력하시겠습니까").trim());
		String danTxt = "quiz01\\"+ dan + "단.txt";
		
			reader = new FileReader(danTxt);
			sc = new Scanner(reader);
			StringBuffer output = new StringBuffer();
			for(int i=1; i<=9;++i) {
			output.append(sc.nextLine()+"\n");
			}
			JOptionPane.showMessageDialog(null, output);	
					
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (NullPointerException e) {
			System.out.println("취소하셨습니다");
		} finally {
			if(null != sc)
			sc.close();
			try {
				if(null != sc)
				reader.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
}
```
