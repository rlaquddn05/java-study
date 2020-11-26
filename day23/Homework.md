### day23.homework
> 학생입력파트는 스캐너로, 사용자메뉴파트는 jop로 작성     

```java
package day23.homework;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.InputMismatchException;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.TreeMap;
import java.util.regex.Pattern;

import javax.swing.JOptionPane;

//< 학생 관리 프로그램 >
//step 1. 다음 학생들의 정보를 Map 에 저장하세요. (TreeMap<Integer,HashMap<String,Object>>)
//key 는 학번(Integer)입니다.
//
//주의) Student 클래스를 사용하지 않고 학생 정보도 Map을 사용합니다. 
//{
//	101 : {"name":"홍길동", "average":88, "grade":"B", "contact":"010-2222-1231"},
//	102 : {"name":"김길동", "average":92, "grade":"A", "contact":"010-2231-1256"},
//	103 : {"name":"김장미", "average":47, "grade":"F", "contact":"010-2512-7754"},
//	...
//}
//
//학번          이름      평균      등급      연락처
//101         홍길동      88       B        010-2222-1231
//102         김길동      92       A        010-2231-1256
//103         김장미      47       F        010-2512-7754
//201         장아름      85       B        010-9966-3512
//202         최영수      74       C        010-1111-3864
//
//step 2. (1)의 딕셔너리에 학생 3명의 정보를 입력 받아 추가 저장합니다.
//    - 학생의 이름, 국, 영, 수, 학년, 연락처를 입력 받습니다.
//
//    - 학년은 학번의 가장 앞자리에 해당합니다.
//      예를 들어 딕셔너리에 저장된 2학년 학생이 4명이라면, 다음 2학년 학생의 학번은 205가 되어야 합니다.
//  (1 <= 학년 <= 6)	
//  (0 <= 학년 당 학생의 수 < 100)
//
//    - 평균은 국,영,수 의 평균을 계산하여 저장합니다.
//        *사용자에게 입력 받지 않습니다.
//
//    - 등급은 평균에 따른 A, B, C, D, F 중 하나로 저장합니다.
//        *사용자에게 입력 받지 않습니다.
//        90 점 이상 : A
//        80점 이상 ~ 90점 미만 : B
//        70점 이상 ~ 80점 미만 : C
//        60점 이상 ~ 70점 미만 : D
//        60점 미만 : F
//
//step 3. 사용자 메뉴를 출력합니다. (선택문제)
//    1. 학번으로 검색
//    2. 연락처 뒷번호로 검색
//    3. 1등 학생 보기
//    4. 모든 학생 보기
//    0. 종료
//
//    1. 학번으로 검색
//        학번을 입력 받고 해당 학생의 모든 정보를 출력합니다.
//        미등록 학번인 경우 '미등록 학번'을 출력합니다.
//
//    2. 연락처 뒷번호로 검색
//        연락처 뒷번호 4자리를 입력 받아 연락처가 일치하는
//        '모든' 학생들의 이름, 학년, 연락처를 출력합니다.
//
//    3. 1등 학생 보기
//        평균을 가지고 1등 학생을 찾아 해당 학생의 학번, 이름, 평균 점수를 출력합니다.
//        공동 1등인 경우 학년이 가장 높은 학생을,
//        그 중 같은 학년에 공동 1등이 있다면 그 학생들 모두를 출력하세요.
//
//    4. 모든 학생 보기
//        현재 등록되어있는 모든 학생들의 모든 정보를 출력하세요.
interface Rules {
	public static final String CONTACT_PATTERN = "^01([0|1|6|7|8|9])-?([0-9]{3,4})-?([0-9]{4})$"; // 전화번호 정규식
	public static final int ADD_STUDENT = 3; // 추가하는 학생의 수, 조정하기 편하도록
}

public class Homework01 implements Rules {
	public TreeMap<Integer, HashMap<String, Object>> id = new TreeMap<>();

	public void menu1() throws NullPointerException, NumberFormatException {
		int idInput = Integer.parseInt(JOptionPane.showInputDialog("찾으시는 학생의 학번을 입력하세요").trim());
		if (id.containsKey(idInput)) {
			JOptionPane.showMessageDialog(null, studentInfo(idInput));
			return;
		} else {
			JOptionPane.showMessageDialog(null, "미등록 학번입니다");
		}
	}

	public void menu2() throws NullPointerException, NumberFormatException {
		String contactLast4 = JOptionPane.showInputDialog("찾으시는 학생의 연락처 뒷자리를 입력하세요").trim();
		int intContactLast4 = Integer.parseInt(contactLast4);
		if (intContactLast4 < 1000 || intContactLast4 > 9999) {
			throw new NumberFormatException();
		}
		StringBuffer infoByContact = new StringBuffer();
		for (Entry<Integer, HashMap<String, Object>> e : id.entrySet()) { // 여러명일 경우 모두 출력하기위해
			String last4 = e.getValue().get("contact").toString().substring(9); // pattern으로 핸드폰번호는 xxx-xxxx-xxxx으로 한정되어
																				// ok
			if (contactLast4.equals(last4)) {
				infoByContact.append(studentInfo(e.getKey()));
			}
		}
		if (infoByContact.length() == 0) {
			JOptionPane.showMessageDialog(null, "미등록 학생입니다");
		} else {
			JOptionPane.showMessageDialog(null, infoByContact);
		}
		return;

	}

	public void menu3() {
		ArrayList<Integer> rank1 = new ArrayList<>(); // 최고점자들을 넣기위한 list
		HashMap<String, Object> temp = new HashMap<>();
		temp.put("average", 0);
		id.put(0, temp); // 초기 비교를위해 학번0, 평균0짜리 학생 만들어 넣음
		rank1.add(0);
		for (Entry<Integer, HashMap<String, Object>> e : id.entrySet()) {
			int lastIdxAvg = (int) (id.get(rank1.get(rank1.size() - 1)).get("average"));
			int eAvg = (int) (e.getValue().get("average"));
			if (lastIdxAvg == eAvg) {
				rank1.add(e.getKey()); // 동점일 경우 list 추가
			} else if (lastIdxAvg < eAvg) {
				rank1.clear();
				rank1.add(e.getKey()); // 새로운 최고점 나오는 경우 list초기화 후 추가
			}
		}
		id.remove(0); // 임시로 넣은 학생 제거

		StringBuffer rank1Info = new StringBuffer();
		int MaxYear = 0; // 동점자가 여럿인 경우 최고학년만을 출력하므로 최고학년을 먼저 찾는다
		for (int i : rank1) {
			if ((i / 100) > MaxYear) {
				MaxYear = (i / 100);
			}
		}
		for (int j : rank1) { // 최고학년과 맞는 최고점자들 출력
			if ((j / 100) == MaxYear) {
				rank1Info.append(studentInfo(j) + "\n");
			}
		}
		JOptionPane.showMessageDialog(null, rank1Info);
	}

	public void menu4() {
		StringBuffer allStudent = new StringBuffer();
		for (Entry<Integer, HashMap<String, Object>> en : id.entrySet()) {
			allStudent.append(studentInfo(en.getKey()) + "\n");
		}
		JOptionPane.showMessageDialog(null, allStudent);
	}

	private int getAverage(int kor, int eng, int math) {
		return (kor + eng + math) / 3;
	}

	private String getGrade(int kor, int eng, int math) {
		switch (getAverage(kor, eng, math) / 10) {
		case 10:
		case 9: {
			return "A";
		}
		case 8: {
			return "B";
		}
		case 7: {
			return "C";
		}
		case 6: {
			return "D";
		}
		default: {
			return "F";
		}
		}

	}

	public String studentInfo(int id) {
		return "학번 : " + id + ", 이름 : " + this.id.get(id).get("name") + ", 평균 : " + this.id.get(id).get("average")
				+ ", 등급 : " + this.id.get(id).get("grade");
	}

	public Homework01() {

		HashMap<String, Object> s1 = new HashMap<>();
		s1.put("name", "홍길동");
		s1.put("average", 88);
		s1.put("grade", "B");
		s1.put("contact", "010-2222-1231");
		id.put(101, s1);

		HashMap<String, Object> s2 = new HashMap<>();
		s2.put("name", "김길동");
		s2.put("average", 92);
		s2.put("grade", "A");
		s2.put("contact", "010-2231-1256");
		id.put(102, s2);

		HashMap<String, Object> s3 = new HashMap<>();
		s3.put("name", "김장미");
		s3.put("average", 47);
		s3.put("grade", "F");
		s3.put("contact", "010-2512-7754");
		id.put(103, s3);

		HashMap<String, Object> s4 = new HashMap<>();
		s4.put("name", "장아름");
		s4.put("average", 85);
		s4.put("grade", "B");
		s4.put("contact", "010-9966-3512");
		id.put(201, s4);

		HashMap<String, Object> s5 = new HashMap<>();
		s5.put("name", "최영수");
		s5.put("average", 74);
		s5.put("grade", "C");
		s5.put("contact", "010-1111-3864");
		id.put(202, s5);

		int[] yearCount = { 3, 2, 0, 0, 0, 0 }; //학번 자동추가위해 각 학년당 인원수를 배열로 저장
		while (true) {
			try {
				for (int i = 1; i <= ADD_STUDENT; ++i) {
					System.out.println("========= " + i + "번째 학생 정보 입력 =========");
					HashMap<String, Object> hm = new HashMap<>();
					Scanner sc = new Scanner(System.in);
					System.out.print("이름 : ");
					String name = sc.next();
					System.out.print("국어 : ");
					int kor = sc.nextInt();
					System.out.print("영어 : ");
					int eng = sc.nextInt();
					System.out.print("수학 : ");
					int math = sc.nextInt();
					System.out.print("학년 : ");
					int year = sc.nextInt();
					if (year < 0 || year > 6) {
						sc.close();
						throw new InputMismatchException();
					}
					System.out.print("연락처 : ");
					String contact = sc.next();
					if (!Pattern.matches(Rules.CONTACT_PATTERN, contact)) {
						sc.close();
						throw new InputMismatchException();
					}
					hm.put("name", name);
					hm.put("average", getAverage(kor, eng, math));
					hm.put("grade", getGrade(kor, eng, math));
					hm.put("contact", contact);
					id.put(year * 100 + yearCount[year - 1] + 1, hm);
					sc.close();
				}
			} catch (InputMismatchException e) {
				System.out.println("올바른 값을 입력하세요, 처음부터 다시 입력받겠습니다.");
				continue;
			}
			break;
		}
		System.out.println("입력 완료! JOP로 넘어갑니다.");

		String menu = "1. 학번으로 검색\n2. 연락처 뒷번호로 검색\n3. 1등 학생 보기\n4. 모든 학생 보기\n0. 종료";

		while (true) {
			try {
				String menuInput = JOptionPane.showInputDialog(null, menu).trim();
				switch (menuInput) {
				case "1": {
					menu1();
					break;

				}
				case "2": {
					menu2();
					break;
				}
				case "3": {
					menu3();
					break;
				}
				case "4": {
					menu4();
					break;
				}
				case "0": {
					JOptionPane.showMessageDialog(null, "프로그램을 종료합니다");
					return;
				}
				default: {
					JOptionPane.showMessageDialog(null, "올바른 메뉴를 선택하세요");
				}
				}
			} catch (NullPointerException e) {
				JOptionPane.showMessageDialog(null, "취소하셨습니다");
				continue;
			} catch (NumberFormatException e) {
				JOptionPane.showMessageDialog(null, "올바른 값을 입력하세요");
				continue;
			}
		}

	}

	public static void main(String[] args) {
		try {
		new Homework01();
		} catch (Throwable e) {
			JOptionPane.showMessageDialog(null, "예상하지 못한 문제발생"); // 혹시 잡아놓지 않은 exception 발생 시
		}
	}
}
```
