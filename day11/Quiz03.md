### day11.Quiz03
#### 메소드 생성 예제3
>  클래스 : Student   
>   필드 : 이름, 국, 영, 수, 평균, 등급   
>   메소드 :    
>     1) setData() : 이름, 국, 영, 수를 인자값으로 받아, 해당 필드에 모두 저장   
>     2) setMean() : 객체가 가지고 있는 국, 영, 수를 가지고 평균을 계산하여 평균 필드에 저장   
>     3) setGrade() : 객체가 가지고 있는 평균을 가지고 등급을 저장    
>        90이상 : A   
>        80이상 ~ 90미만 : B   
>        70이상 ~ 80미만 : C   
>        60이상 ~ 70미만 : D   
>        60미만 : F   
>  	  4) printData() : 객체의 모든 정보(이름, 국, 영, 수, 평균, 등급)를 sysout   
>     
>   메인 클래스 : Quiz03   
>    4명의 학생 객체를 배열로 선언하고    
>    반복문을 사용하여 학생들의 이름, 국, 영, 수를 입력 받음   
>    입력이 끝나면 모든 학생의 정보를 출력   
```java
package day11.quiz;

import java.util.Scanner;

public class Quiz03 {
	public static void main(String[] args) {
		Student [] students = new Student[4];
		Scanner sc = new Scanner(System.in);
		for(int i=0; i<students.length; ++i) {
			students[i] = new Student();
		}

		for(int i=0; i<students.length; ++i) {
			System.out.println("======= 학생 " + (i+1) + "=======");
			System.out.print("국어 점수를 입력하세요 : ");
			int kor = sc.nextInt();
			System.out.print("영어 점수를 입력하세요 : ");
			int eng = sc.nextInt();
			System.out.print("수학 점수를 입력하세요 : ");
			int math = sc.nextInt();
			
			students[i].setData(kor, eng, math);
			students[i].setMean();
			students[i].setGrade();
		}
		sc.close();
		
		for(int i=0; i<students.length; ++i) {
			System.out.println("---- 학생" + (i+1) + " ---- ");
			students[i].printData();
			System.out.println("\n");
			
		}
		
	}
}
```
