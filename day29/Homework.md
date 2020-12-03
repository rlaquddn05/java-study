```java
package day29.homework;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.LayoutManager;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.SimpleDateFormat;
import java.util.Map.Entry;
import java.util.TreeMap;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextArea;

class MyButton extends JButton { // 메뉴
	private String menuName;
	private int price;
	private JTextArea centerPanel;
	private JLabel southLable1;

	MyButton(String menuName, int price, JTextArea centerPanel, JLabel southLable1) {
		super(menuName);
		this.menuName = menuName;
		this.price = price;
		this.centerPanel = centerPanel;
		this.southLable1 = southLable1;
		this.addActionListener(listener);
	}

	ActionListener listener = new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent e) {
			SimpleDateFormat sdf = new SimpleDateFormat("YYYY/MM/dd HH:mm:ss");
			centerPanel.append(menuName + "   " + price + "원  [ " + sdf.format(System.currentTimeMillis()) + " ]\n");
			Homework01.total += price;
			southLable1.setText(Homework01.southLable1Message);
		}
	};
}

class SouthLable2 extends JLabel implements Runnable{

	@Override
	public void run() {
		Homework01 hw = new Homework01();
		SimpleDateFormat sdf = new SimpleDateFormat("YYYY/MM/dd HH:mm:ss");
		while(true) {
			this.setText(sdf.format(System.currentTimeMillis()));
			hw.setVisible(true);
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		
	}
	
}

public class Homework01 extends JFrame { // 메인프레임
	private TreeMap<String, Integer> menu = new TreeMap<>();
	static int total = 0;
	static String southLable1Message = "총  액 : " + total + "원";

	private JPanel southPanel = new JPanel();
	private JPanel northPanel = new JPanel();
	private JPanel westPanel = new JPanel();
	private JButton northButton1 = new JButton("저장하기");
	private JButton northButton2 = new JButton("불러오기");
	private JButton northButton3 = new JButton("결제하기");
	private JLabel southLable1 = new JLabel(southLable1Message);
	private SouthLable2 southLable2 = new SouthLable2();
	private JTextArea centerPanel = new JTextArea();
	public static boolean refresh = false;

	private void setMenu() {
		menu.put("아메리카노", 3500);
		menu.put("카페라떼", 3700);
		menu.put("카푸치노", 3700);
		menu.put("바닐라 라떼", 4000);
		menu.put("카라멜 마끼아또", 4000);
	}

	private void initWestPanel() {
		setMenu();
		westPanel.setLayout(new GridLayout(menu.size(), 1));
		for (Entry<String, Integer> en : menu.entrySet()) {
			westPanel.add(new MyButton(en.getKey(), en.getValue(), centerPanel, southLable1));
		}
	}

	private void initNorthPanel() {
		northPanel.setLayout(new FlowLayout());
		northPanel.add(northButton1);
		northPanel.add(northButton2);
		northPanel.add(northButton3);
	}

	private void initSouthPanel() {
		southPanel.setLayout(new GridLayout(1, 2));
		southLable1.setHorizontalAlignment(JLabel.LEFT);
		southLable2.setHorizontalAlignment(JLabel.RIGHT);
		southPanel.add(southLable1);
		southPanel.add(southLable2);
	}

	private void initCenterPanel() {
	}

	public Homework01() {
		super("포스기 숙제");
		setSize(1200, 800);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLocationRelativeTo(null);

		LayoutManager layout = null;
		layout = new BorderLayout();
		setLayout(layout);

		initWestPanel();
		initNorthPanel();
		initSouthPanel();
//		initCenterPanel(); 나중에 글자 크기조정이나 스크롤바 장착같은거 넣을 수 있도록 만들어 놓음
		add(westPanel, BorderLayout.WEST);
		add(northPanel, BorderLayout.NORTH);
		add(southPanel, BorderLayout.SOUTH);
		add(centerPanel, BorderLayout.CENTER);

		setVisible(true);
		Thread th = new Thread(southLable2);
		th.start();

	}

	public static void main(String[] args) {

		new Homework01();
	}
}
```
