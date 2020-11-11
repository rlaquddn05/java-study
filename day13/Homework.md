### Homework01
#### Student클래스 getter, setter 만들기
##### Student.class
```java
package day13.homework;

public class Student {
	private String name;
	private int kor;
	private int eng;
	private int math;
	private double avg;
	private String grade = "F";
	
	Student(){
	}
	Student(String name){
		this(name, 0, 0, 0 );
	}
	Student(int k, int e, int m){
		this(null, k, e, m );
	}
	Student(String name, int kor, int eng, int math){
		setData(name, kor, eng, math);
	}
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		if( name.length() > 10 ) {
			return;
		}
		this.name=name;
	}
	public int getKor() {
		return kor;
	}
	public void setKor(int kor) {
		if( kor < 0 || kor > 100 ) {
			return;
		}
		this.kor = kor;
		setAvg();
	}
	public int getEng() {
		return eng;
	}
	public void setEng(int eng) {
		if( eng < 0 || eng > 100 ) {
			return;
		}
		this.eng = eng;
		setAvg();
	}
	public int getMath() {
		return math;
	}
	public void setMath(int math) {
		if( math < 0 || math > 100 ) {
			return;
		}
		this.math = math;
		setAvg();
	}
	public double getAvg() {
		return avg;
	}
	private void setAvg() {
		avg = ( kor + eng + math ) / 3.0 ;
		setGrade();
		return;
	}
		
	public String getGrade() {
		return grade;
	}
	private void setGrade() {
		switch((int)(avg/10)) {
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
		
	public void setData(String name, int kor, int eng, int math) {
		setName(name);
		setKor(kor);
		setEng(eng);
		setMath(math);
		return;
	}
	
	private String getData() { 
		return "국어 : " + kor + "\n영어 : " + eng + "\n수학 : " + math + "\n평균 : " + avg + "\n등급 : " + grade;
	}
	
	public void printData() {
		System.out.println(getData());
		}
	
}
```
##### Homework01(Student의 메인메소드)
```java
package day13.homework;

import java.util.Scanner;

public class Homework01 {
	public static void main(String[] args) {
		Student [] students = new Student[4];
		Scanner sc = new Scanner(System.in);
		for(int i=0; i<students.length; ++i) {
			students[i] = new Student();
		}

		for(int i=0; i<students.length; ++i) {
			System.out.println("======= 학생 " + (i+1) + "=======");
			System.out.print("이름을 입력하세요 : ");
			String name = sc.next();
			System.out.print("국어 점수를 입력하세요 : ");
			int kor = sc.nextInt();
			System.out.print("영어 점수를 입력하세요 : ");
			int eng = sc.nextInt();
			System.out.print("수학 점수를 입력하세요 : ");
			int math = sc.nextInt();
			
			students[i].setData(name, kor, eng, math);
			
		}
		sc.close();
		
		for(int i=0; i<students.length; ++i) {
			System.out.println("---- 학생" + (i+1) + " ---- ");
			students[i].printData();
		}
	}
}
```
##### Pokemon.class
```java
package day13.homework;

public class Pokemon {
	
	private String name;
	private int level;
	private int hp;
	private double ap;
	
	Pokemon(){
	}
	Pokemon(String n){
		this(n,0);
	}
	Pokemon(String n, int lv){
		setInfo(n, lv);
	}
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		if ( name.length() > 10 ) {
			return;
		}
		this.name = name;
	}
	public int getLevel() {
		return level;
	}
	public void setLevel(int level) {
		if( level < 0 ) {
			return;
		}
		this.level = level;
		reset();
	}
	public int getHp() {
		return hp;
	}
	public void setHp(int hp) {
		if (hp < 0) {
			return;
		}
		this.hp = hp;
	}
	public double getAp() {
		return ap;
	}
	public void setAp(double ap) {
		this.ap = ap;
	}
	
	private void reset() {
		this.hp = this.level * 1000;
		this.ap = this.level * (int)(Math.random() < 0.8 ? 1.5 : 2 );
	}
	
	public void setInfo(String name, int level) {
		setName(name);
		setLevel(level);
		this.reset();
	}

	public String getInfo() {
		return name + "Lv." + level + "HP." + hp + "AP." + ap;
	}

	public int levelUp() {
		++this.level;
		this.reset();
		return this.level;
	}

	public boolean isAlive() {
		return this.hp > 0;
	}
	public void attack(Pokemon enemy) { // 복합연산자 -= 수행 과정에서 int로 형변환 일어남
		enemy.hp -= this.ap*(Math.random() > 0.1 ? 1.5 : 1);
	}
	
}
```
##### Homework02 (Pokemon의 메인메소드)
```java
package day13.homework;

public class Homework02 {
	public static void main(String[] args) {
		Pokemon p1,p2;
		p1 = new Pokemon();
		p2 = new Pokemon();
		
		p1.setInfo("피카츄", 1);
		p2.setInfo("파이리", 1);
		
		System.out.println(p1.getInfo());
		System.out.println(p2.getInfo());
		
		p1.attack(p2);
		System.out.println(p1.getInfo());
		System.out.println(p2.getInfo());
	}
}
```
