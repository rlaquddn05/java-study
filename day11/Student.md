### Quiz03 메소드 생성 클래스
```java
package day11.quiz;

public class Student {
	String name;
	int kor;
	int eng;
	int math;
	double avg;
	char grade;
	
	void setData(int k, int e, int m) {
		kor = k;
		eng = e;
		math = m;
		return;
	}
	
	void setMean() {
		avg = ( kor + eng + math ) / 3.0 ;
		return;
	}
	
	void setGrade() {
		if(avg >= 90) {
			grade = 'A';
		}
		else if(avg >= 80 && avg <= 90) {
			grade = 'B';
		}
		else if(avg >= 70 && avg <= 80) {
			grade = 'C';
		}
		else if(avg >= 60 && avg <= 70) {
			grade = 'D';
		}
		else grade = 'F';
	}
	
	void printData() {
		System.out.println("국어 : " + kor);
		System.out.println("영어 : " + eng);
		System.out.println("수학 : " + math);
		System.out.println("평균 : " + avg);
		System.out.println("등급 : " + grade);
	}
}
```
