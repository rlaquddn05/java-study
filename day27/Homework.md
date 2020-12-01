### day27.Homework
> Quiz01     
>  	-> 2단.txt ~ 9단.txt 구구단 텍스트 파일 생성     
>  	멀티스레드로 구현하기     

> - 멀티스레드와 싱글스레드를 비교하기 위해 두 코드의 작동시간을 비교해보았다.
> 명확한 비교를 위해 MAX_DAN 설정하여 1000단까지 실행하였다.     
#### < 결과(1000단 수행 기준) >
>  싱글스레드 : 7.5 - 7.6초     
>  멀티스레드 : 0.4 - 0.5초     
>  결론 : 멀티스레드가 훨씬 빠르다

```java
package day27.homework;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;

/*
 * Quiz01
 * 	-> 2단.txt ~ 9단.txt 구구단 텍스트 파일 생성
 * 	멀티스레드로 구현하기
 */
class GugudanThread extends Thread {
	int dan;

	public GugudanThread(int dan) {
		this.dan = dan;
	}

	@Override
	public void run() {
		FileWriter writer=null;
		try {
			writer = new FileWriter("Day27_Homework\\" + dan + "단.txt");
			for (int i = 1; i <= 9; ++i) {
				writer.write(dan + "x" + i + "=" + dan * i + "\n");
			}

		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if(null!=writer)
				writer.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}

	}
}

public class Homework {
	final static int MAX_DAN = 1000;

	public static void main(String[] args) {
		Long t1 = System.currentTimeMillis();
		File folder = new File("Day27_Homework");
		folder.mkdir();
		ArrayList<GugudanThread> gugudans = new ArrayList<>();
		for (int i = 2; i <= MAX_DAN; i++) {
			gugudans.add(new GugudanThread(i));
			gugudans.get(i - 2).start();
		}
		Long t2 = System.currentTimeMillis();
		System.out.println("생성완료! 총 걸린시간 : " + (t2 - t1) / 1000.0 + "초");
	}
}
```

### 기존 Quiz01
> 시간비교 위해 System.currentTimeMillis() 추가    
```java
package day27.quiz;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

/*
 * Quiz01
 * 	-> 2단.txt ~ 9단.txt 구구단 텍스트 파일 생성
 */
public class Quiz01 {
	final static int MAX_DAN = 1000;

	public static void main(String[] args) {
		Long t1 = System.currentTimeMillis();
		FileWriter writer = null;
		File folder = new File("quiz01");
		folder.mkdir();
		for (int i = 2; i <= MAX_DAN; ++i) {
			try {
				String name = "quiz01\\" + i + "단.txt";
				writer = new FileWriter(name);
				for (int j = 1; j <= 9; ++j) {
					writer.write(i + "x" + j + "=" + i * j + "\n");

				}
			} catch (IOException e) {
				e.printStackTrace();
			} finally {
				try {
					if (null != writer)
						writer.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}

		}

		Long t2 = System.currentTimeMillis();
		System.out.println("생성완료! 총 걸린시간 : " + (t2 - t1) / 1000.0 + "초");
	}
}
```
