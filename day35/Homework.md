### 포켓몬 추가/조회
#### 처음부터 GUI로 구현/ 1,2번 모두 GUI로 구현
> < 14일 오전 수정사항 >   
> 입력하지 않는 textfield editable(false)로 변경    
> 입력하지 않고 계산, 추가, 조회 수행할경우 예외처리     
> 레벨에 정수 입력하지 않는 경우 예외처리     
> 
> < 앞으로 수정 희망사항 >    
> 포켓몬추가 패널과 포켓몬 조회 패널 GUI가 상당히 유사한데 일일히 구현함 ---> 코드중복 최소화하는방법 고민해볼 필요 

```java
package day35.homework;

import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;

@SuppressWarnings("serial")
public class Homework01 extends JFrame {

	private static final String URL = "jdbc:mysql://127.0.0.1/testdb";
	private static final String ID = "testdba";
	private static final String PASSWORD = "test1234";
	
	private Connection connection;
	private PreparedStatement preparedStatement;
	private ResultSet resultSet;

	Homework01() {
		super("포켓몬 추가/조회");
		setSize(new Dimension(400, 300));
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setLayout(new GridLayout(1, 2));

		JPanel addPokemon = new JPanel();
		JPanel referencePokemon = new JPanel();

		this.add(addPokemon);
		this.add(referencePokemon);

		addPokemon.setLayout(new BorderLayout());
		JLabel addPokemonLable = new JLabel("포켓몬 추가");
		addPokemonLable.setHorizontalAlignment(JLabel.CENTER);
		addPokemonLable.setFont(new Font("맑은 고딕", Font.BOLD, 20));
		JPanel addPokemonData = new JPanel();

		addPokemon.add(addPokemonLable, BorderLayout.NORTH);
		addPokemon.add(addPokemonData, BorderLayout.CENTER);

		addPokemonData.setLayout(new GridLayout(5, 1));

		JPanel panel1 = new JPanel();
		panel1.setLayout(new BorderLayout());
		panel1.add(new JLabel(" 이름 "), BorderLayout.WEST);
		JTextField textfield1 = new JTextField();
		panel1.add(textfield1, BorderLayout.CENTER);

		addPokemonData.add(panel1);

		JPanel panel2 = new JPanel();
		panel2.setLayout(new BorderLayout());
		panel2.add(new JLabel("  Lv.   "), BorderLayout.WEST);
		JTextField textfield2 = new JTextField();
		panel2.add(textfield2, BorderLayout.CENTER);
		JButton calButton = new JButton("계산");
		panel2.add(calButton, BorderLayout.EAST);
		addPokemonData.add(panel2);

		JPanel panel3 = new JPanel();
		panel3.setLayout(new BorderLayout());
		panel3.add(new JLabel("  HP.   "), BorderLayout.WEST);
		JTextField textfield3 = new JTextField();
		textfield3.setEditable(false);
		panel3.add(textfield3, BorderLayout.CENTER);
		addPokemonData.add(panel3);

		JPanel panel4 = new JPanel();
		panel4.setLayout(new BorderLayout());
		panel4.add(new JLabel("  AP.   "), BorderLayout.WEST);
		JTextField textfield4 = new JTextField();
		textfield4.setEditable(false);
		panel4.add(textfield4, BorderLayout.CENTER);
		addPokemonData.add(panel4);

		calButton.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				try {
				if(textfield2.getText().length()!=0) { // if(textfield2.getText()!="")하면 에러...?
					System.out.println(textfield2.getText());
				int lv = Integer.parseInt(textfield2.getText());
				textfield3.setText(Integer.toString(lv * 100));
				textfield4.setText(Double.toString(lv * 0.5));
				} else {
					JOptionPane.showMessageDialog(Homework01.this, "이름과 레벨을 입력하신 뒤 계산을 수행하세요");
				}
				} catch (NumberFormatException e1) {
					JOptionPane.showMessageDialog(Homework01.this, "레벨은 정수값을 입력하셔야 합니다");
				}
			
			}
		});

		JButton addButton = new JButton("추가");
		addPokemonData.add(addButton);
		addButton.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				if(textfield3.getText().length()!=0) {
				
				try {
					Class.forName("com.mysql.jdbc.Driver");
				} catch (ClassNotFoundException e1) {
					e1.printStackTrace();
				}

				try {
					
					connection = DriverManager.getConnection(URL, ID, PASSWORD);

					String sql = "INSERT INTO pokemon VALUES(NULL, '" + textfield1.getText() + "',"
							+ textfield2.getText() + ", " + textfield3.getText() + "," + textfield4.getText()
							+ ", DEFAULT)";
					System.out.println(sql);
					preparedStatement = connection.prepareStatement(sql);

					preparedStatement.execute();

					System.out.println("저장 완료!");

				} catch (SQLException e1) {
					e1.printStackTrace();
				} finally {
					try {
						if (preparedStatement != null)
							preparedStatement.close();
						if (connection != null)
							connection.close();
					} catch (SQLException e1) {
						e1.printStackTrace();
					}
				}

			} else {
				JOptionPane.showMessageDialog(Homework01.this, "계산을 먼저 수행한 뒤 추가를 해주세요");
			}
			}
		});
		
		referencePokemon.setLayout(new BorderLayout());
		JLabel referencePokemonLable = new JLabel("포켓몬 조회");
		referencePokemonLable.setHorizontalAlignment(JLabel.CENTER);
		referencePokemonLable.setFont(new Font("맑은 고딕", Font.BOLD, 20));
		JPanel referencePokemonData = new JPanel();

		referencePokemon.add(referencePokemonLable, BorderLayout.NORTH);
		referencePokemon.add(referencePokemonData, BorderLayout.CENTER);

		referencePokemonData.setLayout(new GridLayout(5, 1));

		JPanel panel01 = new JPanel();
		panel01.setLayout(new BorderLayout());
		panel01.add(new JLabel(" 이름 "), BorderLayout.WEST);
		JTextField textfield01 = new JTextField();
		panel01.add(textfield01, BorderLayout.CENTER);

		referencePokemonData.add(panel01);

		JPanel panel02 = new JPanel();
		panel02.setLayout(new BorderLayout());
		panel02.add(new JLabel("  Lv.   "), BorderLayout.WEST);
		JTextField textfield02 = new JTextField();
		textfield02.setEditable(false);
		panel02.add(textfield02, BorderLayout.CENTER);
		referencePokemonData.add(panel02);

		JPanel panel03 = new JPanel();
		panel03.setLayout(new BorderLayout());
		panel03.add(new JLabel("  HP.   "), BorderLayout.WEST);
		JTextField textfield03 = new JTextField();
		textfield03.setEditable(false);
		panel03.add(textfield03, BorderLayout.CENTER);
		referencePokemonData.add(panel03);

		JPanel panel04 = new JPanel();
		panel04.setLayout(new BorderLayout());
		panel04.add(new JLabel("  AP.   "), BorderLayout.WEST);
		JTextField textfield04 = new JTextField();
		textfield04.setEditable(false);
		panel04.add(textfield04, BorderLayout.CENTER);
		referencePokemonData.add(panel04);
		
		JButton referencePokemonButton = new JButton("조회");
		referencePokemonData.add(referencePokemonButton);
		referencePokemonButton.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				
				try {
					connection = DriverManager.getConnection(URL, ID, PASSWORD);
					preparedStatement = connection.prepareStatement("SELECT level, hp, ap FROM pokemon WHERE name ='" + textfield01.getText()+"'");
					resultSet = preparedStatement.executeQuery();
				
					while(resultSet.next()) {
						
						textfield02.setText(Integer.toString(resultSet.getInt(1)));
						textfield03.setText(Integer.toString(resultSet.getInt(2)));
						textfield04.setText(Integer.toString(resultSet.getInt(3)));	
			
					}
				if(resultSet.next()==false) { 
					JOptionPane.showMessageDialog(Homework01.this, "미등록 포켓몬");
				}
					
				} catch (SQLException e1) {					
					e1.printStackTrace();
				}
				
			}
		});
		setVisible(true);

	}

	public static void main(String[] args) {
		new Homework01();
	}
}

```
