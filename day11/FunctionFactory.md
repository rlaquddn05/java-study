### 메소드 생성 예제
```java
package day11.quiz;

public class FunctionFactory {
	/* strGugudan()
	 *  인자값 : 정수 1개 
	 *  하는 일 : 해당 구구단 1개의 문자열로 만들기 
	 *  리턴값 : 구구단 문자열 ("2 X 1 = 2 \n2 X 2 = 4 \n2 X 3 = 6\n...")
	 */
	String strGugudan(int dan) {
		String returnString = "";
		for(int i=1; i<=9; ++i) {
			returnString += dan + " x " + i + " = " + i*dan + "\n";
		}
		return returnString;
	}
	
	
	/* printGugudan()
	 *  인자값 : 정수 1개 
	 *  하는 일 : 해당 구구단을 sysout
	 *  리턴값 : 없음
	 */
	void printGugudan(int dan) {
//		for(int i=1; i<=9; ++i) {
//			System.out.println(dan + " x " + i + " = " + i*dan); 
//		}
		System.out.println(strGugudan(dan));
		return;
	}
	
	 /* getAverage()
	 *  인자값 : 국, 영, 수
	 *  하는 일 : 국, 영, 수 평균 계산
	 *  리턴값 : 평균값
	 */
	double getAverage(int kor, int eng, int math) {
		return (kor+eng+math)/3.0;
	}
	
	 /* getRandomPokemon()
	 *  인자값 : X
	 *  하는 일 : "피카츄", "라이츄", "파이리", "꼬부기" 중 1개의 포켓몬을 랜덤으로 뽑기
	 *  		(Math.random() 사용)
	 *  리턴값 : 뽑힌 포켓몬 이름 
	 */
	String getRandomPokemon() {
		String[] names = {"피카츄", "라이츄", "파이리", "꼬부기" };
		return names[(int)(Math.random()*4)];
	}
	
	 /* getMax()
	 *  인자값 : int형 배열 1개 
	 *  하는 일 : 이 배열의 원소 중 가장 큰 수 찾기
	 *  리턴값 : 가장 큰 수
	 */
	int getMax(int[] array) {
		int max=Integer.MIN_VALUE;
		for(int i : array) {
			if (i > max) {
				max = i;
			}
		}
		return max;
	}
}
```
