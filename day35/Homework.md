### 포켓몬 추가/조회
#### 처음부터 GUI로 구현/ 1,2번 모두 GUI로 구현

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
		panel3.add(textfield3, BorderLayout.CENTER);
		addPokemonData.add(panel3);

		JPanel panel4 = new JPanel();
		panel4.setLayout(new BorderLayout());
		panel4.add(new JLabel("  AP.   "), BorderLayout.WEST);
		JTextField textfield4 = new JTextField();
		panel4.add(textfield4, BorderLayout.CENTER);
		addPokemonData.add(panel4);

		calButton.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				int lv = Integer.parseInt(textfield2.getText());
				textfield3.setText(Integer.toString(lv * 100));
				textfield4.setText(Double.toString(lv * 0.5));
			}
		});

		JButton addButton = new JButton("추가");
		addPokemonData.add(addButton);
		addButton.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				try {
					Class.forName("com.mysql.jdbc.Driver");
				} catch (ClassNotFoundException e1) {
					e1.printStackTrace();
				}

				try {
					if (textfield1 == null || textfield2 == null) {
						JOptionPane.showMessageDialog(null, "이름과 레벨을 입력하신 뒤 계산버튼을 눌러주세요");
						throw new NullPointerException();
					}
					if (textfield3 == null || textfield4 == null) {
						JOptionPane.showMessageDialog(null, "체력과 공격력 계산을 먼저 수행하세요");
						throw new NullPointerException();
					}

					connection = DriverManager.getConnection(URL, ID, PASSWORD);

					String sql = "INSERT INTO pokemon VALUES(NULL, '" + textfield1.getText() + "',"
							+ textfield2.getText() + ", " + textfield3.getText() + "," + textfield4.getText()
							+ ", DEFAULT)";
					System.out.println(sql);
					preparedStatement = connection.prepareStatement(sql);

					preparedStatement.execute();

					System.out.println("저장 완료!");

				} catch (NullPointerException e1) {
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
		panel02.add(textfield02, BorderLayout.CENTER);
		referencePokemonData.add(panel02);

		JPanel panel03 = new JPanel();
		panel03.setLayout(new BorderLayout());
		panel03.add(new JLabel("  HP.   "), BorderLayout.WEST);
		JTextField textfield03 = new JTextField();
		panel03.add(textfield03, BorderLayout.CENTER);
		referencePokemonData.add(panel03);

		JPanel panel04 = new JPanel();
		panel04.setLayout(new BorderLayout());
		panel04.add(new JLabel("  AP.   "), BorderLayout.WEST);
		JTextField textfield04 = new JTextField();
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
