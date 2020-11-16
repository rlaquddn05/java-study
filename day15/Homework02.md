### Homework02
#### scan 메소드 추가
```java
package day15.homework2;

import java.util.Scanner;
//부모 클래스 : Student 
//1) 필드 : 학생이름, 나이, 학교명
//2) 메소드 :
//	ㄱ. 생성자 
//		- 디폴트 생성자(기본생성자)
//		- 학생이름, 나이, 학교명 3개 넣고 생성되도록 
//	ㄴ. getters
//	ㄷ. setters
class Student {
	
	private String name;
	private int age;
	private String school;

	public Student() {

	}
	public Student(String name, int age, String school) {
		this.name = name;
		this.age = age;
		this.school = school;
	}

	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		if (age <= 0) {
			return;
		}
		this.age = age;
	}

	public String getSchool() {
		return school;
	}
	public void setSchool(String school) {
		this.school = school;
	}

}

//자식 클래스1 : ElementaryStudent
//1) 추가할 필드 : 국어점수, 영어점수, 학부모 연락처
//2) 메소드 : 
//	ㄱ. 생성자 
//		- 학생이름, 나이, 학교명
//		- 학생이름, 나이, 학교명, 학부모 연락처
//		- 학생이름, 나이, 학교명, 국어점수, 영어점수
//	ㄴ. getters
//	ㄷ. setters
class ElementaryStudent extends Student {
	Scanner sc = new Scanner(System.in);
	private int kor;
	private int eng;
	private String parentTel;
	
	public ElementaryStudent() {
		
	}
	
	public ElementaryStudent(String name, int age) {
		this(name, age, null, 0, 0, null );
	}
	
	public ElementaryStudent(String name, int age, String school, String parentTel) {
		this(name, age, school, 0, 0, parentTel );
	}
		
	public ElementaryStudent(String name, int age, String school, int kor, int eng) {
		this(name, age, school, kor, eng, null );
	}
	
	public ElementaryStudent(String name, int age, String school, int kor, int eng, String parentTel ) {
		super(name, age, school);
		this.kor = kor;
		this.eng = eng;
		this.parentTel = parentTel;
	}

	public int getKor() {
		return kor;
	}
	public void setKor(int kor) {
		if( kor < 0 || kor > 100) {
			return;
		}
		this.kor = kor;
	}

	public int getEng() {
		return eng;
	}
	public void setEng(int eng) {
		if( eng < 0 || eng > 100) {
			return;
		}
		this.eng = eng;
	}

	public String getParentTel() {
		return parentTel;
	}
	public void setParentTel(String parentTel) {
		this.parentTel = parentTel;
	}
	
	public void scan() {
		System.out.print("학교 이름을 입력하세요 : ");
		String school = sc.next();
		System.out.print("국어 점수를 입력하세요 : ");
		int kor = sc.nextInt();
		System.out.print("영어 점수를 입력하세요 : ");
		int eng = sc.nextInt();
		System.out.print("학부모 연락처를 입력하세요 : ");
		sc.nextLine();
		String parentTel = sc.nextLine();
		setSchool(school);
		setKor(kor);
		setEng(eng);
		setParentTel(parentTel);
	}
	
	public String toString () {
		return "이름 : " + getName() + ", 나이 : " + getAge() + ", 학교 : " + getSchool() 
			 + "\n국어 : " + kor + ", 영어 : " + eng 
			 + "\n학부모 연락처 : " + getParentTel();
	}
	
}
//자식 클래스2 : MiddleSchoolStudent
//1) 추가할 필드 : 국어점수, 영어점수, 수학점수, 평균점수		
//2) 메소드 : 
//	ㄱ. 생성자 
//		- 학생이름, 나이, 학교명, 국어점수, 영어점수, 수학점수
//		  (평균 자동 계산)
//	ㄴ. getters
//	ㄷ. setters
class MiddleSchoolStudent extends Student {
	Scanner sc = new Scanner(System.in);
	private int kor;
	private int eng;
	private int math;
	private double avg;
	
	
	public MiddleSchoolStudent() {
		
	}
	public MiddleSchoolStudent(String name, int age) {
		this(name, age, null, 0, 0, 0);
	}
	public MiddleSchoolStudent(String name, int age, String school, int kor, int eng, int math) {
		super(name, age, school);
		setKor(kor);
		setEng(eng);
		setMath(math);
		setAvg();
	}
	
	public int getKor() {
		return kor;
	}
	public void setKor(int kor) {
		if( kor < 0 || kor > 100) {
			return;
		}	
		this.kor = kor;
		setAvg();
	}
	public int getEng() {
		return eng;
	}
	public void setEng(int eng) {
		if( eng < 0 || eng > 100) {
			return;
		}
		this.eng = eng;
		setAvg();
	}
	public int getMath() {
		return math;
	}
	public void setMath(int math) {
		if( math < 0 || math > 100) {
			return;
		}
		this.math = math;
		setAvg();
	}
	public double getAvg() {
		return avg;
	}
	private void setAvg() {
		this.avg = ( this.kor + this.eng + this.math ) / 3.0;
	}
	
	public void scan() {
		System.out.print("학교 이름을 입력하세요 : ");
		String school = sc.next();
		System.out.print("국어 점수를 입력하세요 : ");
		int kor = sc.nextInt();
		System.out.print("영어 점수를 입력하세요 : ");
		int eng = sc.nextInt();
		System.out.print("수학 점수를 입력하세요 : ");
		int math = sc.nextInt();
		setSchool(school);
		setKor(kor);
		setEng(eng);
		setMath(math);
	}
	
	public String toString () {
		return "이름 : " + getName() + ", 나이 : " + getAge() + ", 학교 : " + getSchool() 
			 + "\n국어 : " + getKor() + ", 영어 : " + getEng() + ", 수학 : " + getMath() 
			 + "\n평균 : " + getAvg();
	}
		
}

//자식 클래스3 : HighSchoolStudent
//1) 추가할 필드 : 국어점수, 영어점수, 수학점수, 평균점수, 내신등급	
//2) 메소드 : 
//	ㄱ. 생성자 
//		- 학생이름, 나이, 학교명, 국어점수, 영어점수, 수학점수
//		  (평균 자동 계산)
//	ㄴ. getters
//	ㄷ. setters
class HighSchoolStudent extends MiddleSchoolStudent {
	private String grade ;

	public HighSchoolStudent() {
		
	}
	public HighSchoolStudent(String name, int age) {
		super(name, age);
	}
	public HighSchoolStudent(String name, int age, String school, int kor, int eng, int math) {
		super(name, age, school, kor, eng, math);
		setGrade();
	}
	
	public String getGrade() {
		return grade;
	}
	private void setGrade() {
		switch((int)(getAvg()/10)) {
		case 10 :
		case 9 : {
			grade = "A";
			break;
		}
		case 8 :{
			grade = "B";
			break;
		}
		case 7 :{
			grade = "C";
			break;
		}
		case 6 :{
			grade = "D";
			break;
		}
		default :
			break;
		}
	}
	
	public void scan() {
		super.scan();
		setGrade();
	}
	
	public String toString () {
		return "이름 : " + getName() + ", 나이 : " + getAge() + ", 학교 : " + getSchool() 
			 + "\n국어 : " + getKor() + ", 영어 : " + getEng() + ", 수학 : " + getMath() 
			 + "\n평균 : " + getAvg() + ", 등급 : " + getGrade() ;
	}
}
//메인 클래스 : Quiz02
//- 이름과 나이를 입력 받음
//- 나이에 따른 객체 생성 (예. 13 -> new ElementaryStudent())
//- 각 객체의 필드를 입력 받아서 저장 
//예. 중학생이면
//	  학교명, 국어점수, 영어점수, 수학점수 입력 받음
//- 결과 출력
public class Homework01 {
	
	public Homework01() {
		Scanner sc = new Scanner(System.in);
		System.out.print("이름을 입력하세요 : ");
		String name = sc.next();
		System.out.print("나이를 입력하세요 : ");
		int age = sc.nextInt();
		
		switch(age) {
		case 8 :
		case 9 :
		case 10 :
		case 11 :
		case 12 :
		case 13 : {
			ElementaryStudent eStudent = new ElementaryStudent(name, age);
			eStudent.scan();
			System.out.println(eStudent);
			break;
		}
		case 14 :
		case 15 :
		case 16 : {
			MiddleSchoolStudent mStudent = new MiddleSchoolStudent(name, age);
			mStudent.scan();
			System.out.println(mStudent);
			break;
		}
		case 17 :
		case 18 :
		case 19 : {
			HighSchoolStudent hStudent = new HighSchoolStudent(name, age);
			hStudent.scan();
			System.out.println(hStudent);
			break;
		}
		default : {
			System.out.println("학생이 아닙니다.");
			break;
		}
		}//스위치
		sc.close();
	}

	public static void main(String[] args) {
		new Homework01();
	}//메인
}//클래스
```
