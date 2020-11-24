### day22.Homework
```java
package day22.homework;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map.Entry;

import javax.swing.JOptionPane;

//String menu = "1. 단어 추가\n" 
//		+ "2. 단어 검색\n" 
//		+ "3. 모든 단어 보기\n"
//		+ "4. 퀴즈 풀기 \n"
//		+ "0. 종료\n입력 : ";
//1 : 영단어, 그의 뜻(한글) 을 입력 받고 단어장(Map)에 저장
//2 : 영단어 입력 받고 그의 뜻을 출력. 없으면 "미등록 단어" 출력  (containsKey("apple")) 
//3 : for문 사용 
//4 : (선택문제) 
//      문제 : 뜻   / 답 : 영단어  
//예) 사과(은)는 영어로? ==> 'home' 입력 ==> 땡!
//문제는 랜덤하게 나와야 함. Map --> List 나 array 로 변경해야 함

public class Homework01 {
	public static void main(String[] args) {
		String menu = "1. 단어 추가\n2. 단어 검색\n3. 모든 단어 보기\n4. 퀴즈 풀기 \n0. 종료";
		HashMap<String, String> words = new HashMap<>();
		while (true) {
			String menuInput = JOptionPane.showInputDialog(null, menu);
			if (menuInput == null) { // 메뉴창에서 x, 취소 누르는것 방지
				continue;
			}
			switch (menuInput.trim()) {
			case "1": {
				String word = JOptionPane.showInputDialog("영단어 : ");
				if (word == null) {
					JOptionPane.showMessageDialog(null, "취소하셨습니다");
					break;
				}
				String meaning = JOptionPane.showInputDialog("뜻 : ");
				if (meaning == null) {
					JOptionPane.showMessageDialog(null, "취소하셨습니다");
					break;
				}
				words.put(word.trim(), meaning.trim());
				break;

			}
			case "2": {
				if (words.isEmpty()) {
					JOptionPane.showMessageDialog(null, "단어를 먼저 추가하세요");
					break;
				}
				String searchWord = JOptionPane.showInputDialog("검색하실 단어를 입력하세요");
				if (searchWord == null) {
					JOptionPane.showMessageDialog(null, "취소하셨습니다");
					break;
				}
				if (words.containsKey((String)searchWord.trim())) {
					JOptionPane.showMessageDialog(null, searchWord + " : " + words.get(searchWord));
					continue;
				}
				JOptionPane.showMessageDialog(null, "없는 단어입니다");
				break;
			}
			case "3": {
				if (words.isEmpty()) {
					JOptionPane.showMessageDialog(null, "단어를 먼저 추가하세요");
					break;
				}
				StringBuffer allWords = new StringBuffer("");
				for (Entry<String, String> en : words.entrySet()) {
					allWords.append(en.getKey() + " : " + en.getValue() + "\n");
				}
				JOptionPane.showMessageDialog(null, allWords);
				break;
			}
			case "4": {
				if (words.isEmpty()) {
					JOptionPane.showMessageDialog(null, "단어를 먼저 추가하세요");
					break;
				}
				ArrayList<String> wordList = new ArrayList<>(words.values());
				String question = wordList.get((int) (Math.random() * wordList.size()));
				String ans = JOptionPane.showInputDialog(question);
				if (ans == null) {
					JOptionPane.showMessageDialog(null, "취소하셨습니다");
					break;
				}
				JOptionPane.showMessageDialog(null, question.equals(words.get(ans.trim())) ? "정답!" : "땡!");
				break;
			}
			case "0": {
				return;
			}
			default: {
				JOptionPane.showMessageDialog(null, "올바른 메뉴를 선택하세요");
			}
			}
		}
	}
}
```
