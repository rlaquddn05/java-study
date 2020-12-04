### 길찾기게임
```java
package day30.homework;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.GridLayout;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class Homework01 extends JFrame {

	private static final int ROAD = 0;
	private static final int WALL = 1;
	private static final int CURRENT = 2;
	private static final int END = 3;
	private static final int START = 4;
	private static final int[][] map = { { CURRENT, ROAD, WALL, WALL, WALL, ROAD, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD }, { WALL, WALL, WALL, ROAD, ROAD, ROAD, ROAD, ROAD },
			{ WALL, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD }, { WALL, WALL, WALL, ROAD, WALL, WALL, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, WALL, END }, { ROAD, WALL, WALL, WALL, WALL, WALL, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD }, };
	private static final Color[] COLOR = { new Color(255, 255, 255), new Color(0, 0, 0), new Color(255, 0, 0),
			new Color(0, 0, 255) };

	private int x = 0;
	private int y = 0;

	static class MyButton extends JButton {
		private int stat;

		public MyButton(int stat, int i, int j) {
			this.stat = stat;
			setButtonColor();
			setText(i + "," + j);
		}

		private void setButtonColor() {
			this.setBackground(COLOR[stat]);
		}

	}

	Homework01() {
		super("길찾기");
		setSize(new Dimension(500, 500));
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setLayout(new GridLayout(8, 8));

		MyButton[][] buttons = new MyButton[8][8];
		for (int i = 0; i < 8; ++i) {
			for (int j = 0; j < 8; ++j) {
				buttons[i][j] = new MyButton(map[i][j], i, j);
				buttons[i][j].setEnabled(false);
				this.add(buttons[i][j]);
			}

		}

		this.addKeyListener(new KeyListener() {
			@Override
			public void keyTyped(KeyEvent e) {
			}

			@Override
			public void keyReleased(KeyEvent e) {
			}

			@Override
			public void keyPressed(KeyEvent e) {
				if (e.getKeyCode() == KeyEvent.VK_UP) {
					y -= 1;
					try {
						if (buttons[y][x].stat == 0) {
							buttons[y][x].stat = 2;
							buttons[y][x].setButtonColor();
							buttons[y + 1][x].stat = 0;
							buttons[y + 1][x].setButtonColor();
						} else if (buttons[y][x].stat == 3) {
							JOptionPane.showMessageDialog(null, "WIN!");
							System.exit(0);
						} else {
							y += 1;
						}
					} catch (ArrayIndexOutOfBoundsException e1) {
						y += 1;
					}
				} else if (e.getKeyCode() == KeyEvent.VK_DOWN) {
					y += 1;
					try {
						if (buttons[y][x].stat == 0) {
							buttons[y][x].stat = 2;
							buttons[y][x].setButtonColor();
							buttons[y - 1][x].stat = 0;
							buttons[y - 1][x].setButtonColor();
						} else if (buttons[y][x].stat == 3) {
							JOptionPane.showMessageDialog(null, "WIN!");
							System.exit(0);
						} else {
							y -= 1;
						}
					} catch (ArrayIndexOutOfBoundsException e1) {
						y -= 1;
					}
				}

				else if (e.getKeyCode() == KeyEvent.VK_RIGHT) {
					x += 1;
					try {
						if (buttons[y][x].stat == 0) {
							buttons[y][x].stat = 2;
							buttons[y][x].setButtonColor();
							buttons[y][x - 1].stat = 0;
							buttons[y][x - 1].setButtonColor();
						} else if (buttons[y][x].stat == 3) {
							JOptionPane.showMessageDialog(null, "WIN!");
							System.exit(0);
						} else {
							x -= 1;
						}
					} catch (ArrayIndexOutOfBoundsException e1) {
						x -= 1;
					}
				} else if (e.getKeyCode() == KeyEvent.VK_LEFT) {
					x -= 1;
					try {
						if (buttons[y][x].stat == 0) {
							buttons[y][x].stat = 2;
							buttons[y][x].setButtonColor();
							buttons[y][x + 1].stat = 0;
							buttons[y][x + 1].setButtonColor();
						} else if (buttons[y][x].stat == 3) {
							JOptionPane.showMessageDialog(null, "WIN!");
							System.exit(0);
						} else {
							x += 1;
						
						
						}
					} catch (ArrayIndexOutOfBoundsException e1) {
						x += 1;
					}

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
