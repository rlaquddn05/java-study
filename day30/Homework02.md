### 달력만들기
> - 추가해야할것 : 아직 날짜입력을 안함, 월 입력시 달력페이지 바뀌는것도 하고싶은데 아직안함   
> - 수정하고싶은것 : 현재 daybutton마다 actionlistener 가 달려 있는데 하나로 해결하고싶은데 panel이나 frame은 actionlistener부착이 안됨..
> - 현재 진행상황 : 1. 달력외형, popup외형      
> 		   2. popup에서 save버튼 누르면 내용이 날짜이름으로 저장됨     
>		   3. 달력에서 날짜 누르면 pop이 뜰 때 세이브파일이 있으면 불러옴     

```java
package day30.homework;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.util.ArrayList;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextField;
import javax.swing.border.EmptyBorder;
import javax.swing.border.LineBorder;

class popup extends JFrame {
	int date;
	JLabel dateLabel = new JLabel();
	JLabel todoLabel = new JLabel("  < To do >");
	JTextField todoTextField1 = new JTextField(" 1. ");
	JTextField todoTextField2 = new JTextField(" 2. ");
	JTextField todoTextField3 = new JTextField(" 3. ");
	JLabel memoLabel = new JLabel("  < Memo >");
	JTextField memoTextField = new JTextField();
	JButton clear = new JButton("clear");
	JButton save = new JButton("save");

	public void setPopup() {
		setSize(new Dimension(500, 700));
		setDefaultCloseOperation(DISPOSE_ON_CLOSE);
		setLayout(new BorderLayout());

		dateLabel.setText(Integer.toString(this.date));
		dateLabel.setHorizontalAlignment(JLabel.CENTER);
		dateLabel.setFont(new Font("맑은 고딕", Font.BOLD, 30));
		JPanel panel = new JPanel();
		panel.setLayout(new BorderLayout(5, 5));
		this.add(dateLabel, BorderLayout.NORTH);
		this.add(panel, BorderLayout.CENTER);

		JPanel todoPanel = new JPanel();
		JPanel memoPanel = new JPanel();
		JPanel buttonsPanel = new JPanel();
		todoPanel.setBorder(new LineBorder(new Color(0, 0, 0), 3));
		memoPanel.setBorder(new LineBorder(new Color(0, 0, 0), 3));
		panel.add(todoPanel, BorderLayout.NORTH);
		panel.add(memoPanel, BorderLayout.CENTER);
		panel.add(buttonsPanel, BorderLayout.SOUTH);

		todoLabel.setFont(new Font("맑은 고딕", Font.BOLD, 15));
		todoLabel.setOpaque(true);
		todoLabel.setBackground(new Color(134, 217, 252));
		todoTextField1.setBorder(new EmptyBorder(0, 0, 0, 0));
		todoTextField1.setFont(new Font("맑은 고딕", Font.PLAIN, 15));
		todoTextField2.setBorder(new EmptyBorder(0, 0, 0, 0));
		todoTextField2.setFont(new Font("맑은 고딕", Font.PLAIN, 15));
		todoTextField3.setBorder(new EmptyBorder(0, 0, 0, 0));
		todoTextField3.setFont(new Font("맑은 고딕", Font.PLAIN, 15));

		todoPanel.setLayout(new GridLayout(4, 1));
		todoPanel.setBackground(new Color(255, 255, 255));
		todoPanel.add(todoLabel);
		todoPanel.add(todoTextField1);
		todoPanel.add(todoTextField2);
		todoPanel.add(todoTextField3);

		memoLabel.setFont(new Font("맑은 고딕", Font.BOLD, 15));
		memoLabel.setOpaque(true);
		memoLabel.setBackground(new Color(134, 217, 252));

		memoPanel.setLayout(new BorderLayout());
		memoPanel.add(memoLabel, BorderLayout.NORTH);
		memoPanel.add(memoTextField, BorderLayout.CENTER);

		buttonsPanel.setLayout(new FlowLayout());
		
		// clear버튼 누르면 todo목록과 memo 초기화
		clear.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				todoTextField1.setText(" 1. ");
				todoTextField2.setText(" 2. ");
				todoTextField3.setText(" 3. ");
				memoTextField.setText(null);
			}
		});
		
		// save버튼 누르면 daybuttons에 todo 목록의 내용 text입력
		// 				날짜이름으로 todo목록과 memo내용 세이브파일 생성
		save.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				File folder = new File("달력프로그램\\12월");
				folder.mkdir();
				(Homework02.dayButtons[Homework02.popup.date]).setText("<html>" + todoTextField1.getText() + "<br>"
						+ todoTextField2.getText() + "<br>" + todoTextField3.getText() + "<br>");
				Homework02.info.clear();
				Homework02.info.add(todoTextField1.getText());
				Homework02.info.add(todoTextField2.getText());
				Homework02.info.add(todoTextField3.getText());
				Homework02.info.add(memoTextField.getText());

				try (FileOutputStream fOut = new FileOutputStream("달력프로그램\\12월\\" + dateLabel.getText());
						ObjectOutputStream oOut = new ObjectOutputStream(fOut);) {
					oOut.writeObject(Homework02.info);
				} catch (Exception e1) {
					e1.printStackTrace();
				}

			}
		});
		buttonsPanel.add(clear);
		buttonsPanel.add(save);

	}

	popup() {
		super();
	}
}

class DayButton extends JButton {
	int date;

	DayButton() {
	}

	DayButton(int date) {
		this.date = date;
	}
}

@SuppressWarnings("serial")
public class Homework02 extends JFrame {
	private JLabel monthLabel = new JLabel("12월");
	public static DayButton[] dayButtons = new DayButton[42];
	public static popup popup = new popup();
	public static ArrayList<String> info = new ArrayList<>();

	Homework02() {
		super("달력");
		setSize(new Dimension(900, 700));
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setLayout(new BorderLayout());

		monthLabel.setFont(new Font("맑은 고딕", Font.BOLD, 50));
		monthLabel.setHorizontalAlignment(JLabel.CENTER);
		this.add(monthLabel, BorderLayout.NORTH);

		JPanel sunToSatPanel = new JPanel();
		JPanel daysPanel = new JPanel();
		JPanel panel = new JPanel();
		sunToSatPanel.setLayout(new GridLayout(1, 7));
		daysPanel.setLayout(new GridLayout(6, 7));
		panel.setLayout(new BorderLayout());
		panel.add(sunToSatPanel, BorderLayout.NORTH);
		panel.add(daysPanel, BorderLayout.CENTER);
		this.add(panel, BorderLayout.CENTER);

		JLabel[] sunToSat = new JLabel[7];
		String[] ssunToSat = { "일", "월", "화", "수", "목", "금", "토" };
		for (int i = 0; i < 7; ++i) {
			sunToSat[i] = new JLabel(ssunToSat[i]);
			sunToSat[i].setBorder(new LineBorder(new Color(0, 0, 0), 1));
			sunToSat[i].setHorizontalAlignment(JLabel.CENTER);
			sunToSat[i].setFont(new Font("맑은 고딕", Font.BOLD, 25));
		}
		sunToSat[0].setForeground(new Color(255, 0, 0));
		sunToSat[6].setForeground(new Color(0, 0, 255));
		for (int i = 0; i < 7; ++i) {
			sunToSatPanel.add(sunToSat[i]);
		}

		JPanel[] dayPanel = new JPanel[42];
		JLabel[] dayLabel = new JLabel[42];

		popup.setPopup();
		for (int i = 0; i < 42; ++i) {
			dayPanel[i] = new JPanel();
			dayPanel[i].setLayout(new BorderLayout());

			dayLabel[i] = new JLabel(i + "칸");
			dayLabel[i].setFont(new Font("맑은 고딕", Font.BOLD, 15));
			dayLabel[i].setHorizontalAlignment(JLabel.RIGHT);
			dayButtons[i] = new DayButton(i);
			dayButtons[i].setBorder(new EmptyBorder(0, 0, 0, 0));
			dayButtons[i].setBackground(new Color(255, 255, 255));
			
			// daybuttons 누르면 해당일의 save파일이 있으면 불러옴, 없으면 초기화된 popup
			dayButtons[i].addActionListener(new ActionListener() {
				@Override
				public void actionPerformed(ActionEvent e) {
					popup.date = ((DayButton) e.getSource()).date;
					popup.dateLabel.setText(Integer.toString(popup.date));
					try (FileInputStream fIn = new FileInputStream("달력프로그램\\12월\\" + popup.dateLabel.getText());
							ObjectInputStream oIn = new ObjectInputStream(fIn);) {
						info = (ArrayList<String>) oIn.readObject();
						popup.todoTextField1.setText(info.get(0));
						popup.todoTextField2.setText(info.get(1));
						popup.todoTextField3.setText(info.get(2));
						popup.memoTextField.setText(info.get(3));
					} catch (FileNotFoundException e1) {
						popup.todoTextField1.setText(" 1. ");
						popup.todoTextField2.setText(" 2. ");
						popup.todoTextField3.setText(" 3. ");
						popup.memoTextField.setText(null);
					} catch (Exception e1) {
						e1.printStackTrace();
					}

					popup.setVisible(true);
				}
			});

			dayPanel[i].add(dayLabel[i], BorderLayout.NORTH);
			dayPanel[i].add(dayButtons[i], BorderLayout.CENTER);
			dayPanel[i].setBorder(new LineBorder(new Color(0, 0, 0), 1));

			daysPanel.add(dayPanel[i]);
		}
		
		//프로그램 켤 때 day버튼에 todo를 붙여넣음
		File directory = new File("달력프로그램\\12월");
		File[] files = directory.listFiles();
		for (File f : files) {
			try (FileInputStream fIn = new FileInputStream(f); ObjectInputStream oIn = new ObjectInputStream(fIn);) {
				info = (ArrayList<String>) oIn.readObject();
				(dayButtons[Integer.parseInt(f.getName())])
						.setText("<html>" + info.get(0) + "<br>" + info.get(1) + "<br>" + info.get(2) + "<br>");

			} catch (Exception e1) {
				e1.printStackTrace();
			}
		}

		setVisible(true);
	}

	public static void main(String[] args) {
		new Homework02();
	}
}
```
![달력](https://user-images.githubusercontent.com/73927722/101273519-7bd63980-37d9-11eb-85dc-7aba67f2477d.JPG)
![popup](https://user-images.githubusercontent.com/73927722/101273520-7c6ed000-37d9-11eb-9b2f-5934f9251056.JPG)

