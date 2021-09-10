# Rhythm_Game_with_Java
To get used to Java, create rhythm game with my favorite song

~~
2021.09.10
(add 6 song, making beats_)



Add just in case (need to revise)


Dynamic Beat.java


package dynamic_beat_17_스코어;

import java.awt.Color;
import java.awt.Cursor;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionAdapter;
import java.util.ArrayList;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame; // Made by 'ctrl+shift+o' 
import javax.swing.JLabel;

public class DynamicBeat extends JFrame {

	private Image screenImage;
	private Graphics screenGraphic;
	
	private ImageIcon exitButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/exitButtonEntered.png"));
	private ImageIcon exitButtonBasicImage = new ImageIcon(Main.class.getResource("../images/exitButtonBasic.png"));
	private ImageIcon startButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/startButtonEntered.png"));
	private ImageIcon startButtonBasicImage = new ImageIcon(Main.class.getResource("../images/startButtonBasic.png"));
	private ImageIcon quitButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/quitButtonEntered.png"));
	private ImageIcon quitButtonBasicImage = new ImageIcon(Main.class.getResource("../images/quitButtonBasic.png"));
	private ImageIcon leftButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/leftButtonEntered.png"));
	private ImageIcon leftButtonBasicImage = new ImageIcon(Main.class.getResource("../images/leftButtonBasic.png"));
	private ImageIcon rightButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/rightButtonEntered.png"));
	private ImageIcon rightButtonBasicImage = new ImageIcon(Main.class.getResource("../images/rightButtonBasic.png"));
	private ImageIcon easyButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/easyButtonEntered.png"));
	private ImageIcon easyButtonBasicImage = new ImageIcon(Main.class.getResource("../images/easyButtonBasic.png"));
	private ImageIcon hardButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/hardButtonEntered.png"));
	private ImageIcon hardButtonBasicImage = new ImageIcon(Main.class.getResource("../images/hardButtonBasic.png"));
	private ImageIcon backButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/backButtonEntered.png"));
	private ImageIcon backButtonBasicImage = new ImageIcon(Main.class.getResource("../images/backButtonBasic.png"));
	private ImageIcon infoButtonBasicImage = new ImageIcon(Main.class.getResource("../images/infoBasicImage.png"));	
	private ImageIcon infoButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/infoEnteredImage.png"));	
	private ImageIcon infoBackButtonBasicImage = new ImageIcon(Main.class.getResource("../images/infoBackBasicImage.png"));	
	private ImageIcon infoBackButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/infoBackEnteredImage.png"));	

	
	//private Image scoreImage = new ImageIcon(Main.class.getResource("../images/scoreImage.png")).getImage();
	private ImageIcon scoreButtonBasicImage = new ImageIcon(Main.class.getResource("../images/scoreButtonBasicImage.png"));
	private ImageIcon scoreButtonEnteredImage = new ImageIcon(Main.class.getResource("../images/scoreButtonEnteredImage.png"));
	private ImageIcon scoreSImage = new ImageIcon(Main.class.getResource("../images/scoreS.png"));
	private ImageIcon scoreAImage = new ImageIcon(Main.class.getResource("../images/scoreA.png"));
	private ImageIcon scoreBImage = new ImageIcon(Main.class.getResource("../images/scoreB.png"));
	private ImageIcon scoreCImage = new ImageIcon(Main.class.getResource("../images/scoreC.png"));

	
	
	
	
	
	private Image background = new ImageIcon(Main.class.getResource("../images/introBackground(title).jpg"))
			.getImage();
	private JLabel menuBar = new JLabel(new ImageIcon(Main.class.getResource("../images/menuBar.png")));
	
	private JButton exitButton = new JButton(exitButtonBasicImage);
	private JButton startButton = new JButton(startButtonBasicImage);
	private JButton quitButton = new JButton(quitButtonBasicImage);
	private JButton leftButton = new JButton(leftButtonBasicImage);
	private JButton rightButton = new JButton(rightButtonBasicImage);
	private JButton easyButton = new JButton(easyButtonBasicImage);
	private JButton hardButton = new JButton(hardButtonBasicImage);
	private JButton backButton = new JButton(backButtonBasicImage);
	private JButton infoButton = new JButton(infoButtonBasicImage);
	private JButton infoBackButton = new JButton(infoBackButtonBasicImage);
	private JButton scoreButton = new JButton(scoreButtonBasicImage);
	private JButton scoreS = new JButton(scoreSImage);
	private JButton scoreA = new JButton(scoreAImage);
	private JButton scoreB = new JButton(scoreBImage);
	private JButton scoreC = new JButton(scoreCImage);
	
	
	private int mouseX, mouseY; // coordinates of mouse
	
	private boolean isMainScreen = false;
	private boolean isGameScreen = false;
	
	ArrayList<Track> trackList = new ArrayList<Track>();
	
	

	private Image titleImage;
	private Image selectedImage;
	private Music selectedMusic;
	private Music introMusic = new Music("introMusic.mp3", true); // music played (계속)
	private int nowSelected = 0;
	
	public static Game game;
	
	/*public endMusic() {
		if (game.isMusicEnd())
		{
			showScore();
			//
		}
	}*/
	
	public DynamicBeat() { // constructor

		//0 index
		trackList.add(new Track("Wild World Title Image.png", "Wild World Start Image.png",
				"Wild World Game Image.png", "Wild World.mp3", "Wild World.mp3", "Wild World"));		
		//1 index
		trackList.add(new Track("Temple of Time Title Image.png", "Temple of Time Start Image.png",
				"Temple of Time Game Image.png", "Temple of Time Selected.mp3", "Temple of Time.mp3", "Temple of Time"));
		//2 index
		trackList.add(new Track("The Cygnus Garden Title Image.png", "The Cygnus Garden Start Image.png",
				"The Cygnus Garden Game Image.png", "The Cygnus Garden Selected.mp3", "The Cygnus Garden.mp3", "The Cygnus Garden"));
		//3 index
		trackList.add(new Track("Shattered Time Title Image.png", "Shattered Time Start Image.png",
				"Shattered Time Game Image.png", "Shattered Time Selected.mp3", "Shattered Time.mp3", "Shattered Time"));
		//4 index
		trackList.add(new Track("The Tune of The Azure Light Title Image.png", "The Tune of The Azure Light Start Image.png",
				"The Tune of The Azure Light Game Image.png", "The Tune of The Azure Light Selected.mp3", "The Tune of The Azure Light.mp3", "The Tune of The Azure Light"));
		//5
		trackList.add(new Track("Kamado Tanjiro No Uta Title Image.png", "Kamado Tanjiro No Uta Start Image.png",
				"Kamado Tanjiro No Uta Game Image.png", "Kamado Tanjiro No Uta Selected.mp3", "Kamado Tanjiro No Uta.mp3", "Kamado Tanjiro No Uta"));
		
		
		/*
		 * 게임 환경 설정 http://wallpaperswide.com
		 */
		setUndecorated(true);
		setTitle("Dynamic Beat"); // set game title name
		setSize(Main.SCREEN_WIDTH, Main.SCREEN_HEIGHT); // set size of the game
		setResizable(false); // not allow users to adjust size of the game
		setLocationRelativeTo(null); // appear game in the middle of the screen
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // exit game
		setVisible(true); // successfully appear on the screen
		setBackground(new Color(0, 0, 0, 0)); // white
		setLayout(null);
		
		addKeyListener(new KeyListener());
		
		
		// Music
		
		introMusic.start();
		
		
		
		
		//ExitButton
		exitButton.setBounds(1245, 0, 30, 30);
		// make button layout clear
		exitButton.setBorderPainted(false);
		exitButton.setContentAreaFilled(false);
		exitButton.setFocusPainted(false);
		exitButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				exitButton.setIcon(exitButtonEnteredImage);
				exitButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				exitButton.setIcon(exitButtonBasicImage);
				exitButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }
				 
				System.exit(0);
				
			}
		});
		
		add(exitButton);
		
		
		
		//StartButton
		startButton.setBounds(40, 200, 400, 100);
		// make button layout clear
		startButton.setBorderPainted(false);
		startButton.setContentAreaFilled(false);
		startButton.setFocusPainted(false);
		startButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				startButton.setIcon(startButtonEnteredImage);
				startButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				startButton.setIcon(startButtonBasicImage);
				startButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }
				
				//게임 시작 이벤트
				enterMain();
				
			}
		});
		
		add(startButton);
		

		
		//StartButton
		quitButton.setBounds(40, 330, 400, 100);
		// make button layout clear
		quitButton.setBorderPainted(false);
		quitButton.setContentAreaFilled(false);
		quitButton.setFocusPainted(false);
		quitButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				quitButton.setIcon(quitButtonEnteredImage);
				quitButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				quitButton.setIcon(quitButtonBasicImage);
				quitButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }
				System.exit(0);
			}
		});
		
		add(quitButton);
		
		

		leftButton.setVisible(false);
		leftButton.setBounds(140, 310, 100, 100);
		// make button layout clear
		leftButton.setBorderPainted(false);
		leftButton.setContentAreaFilled(false);
		leftButton.setFocusPainted(false);
		leftButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				leftButton.setIcon(leftButtonEnteredImage);
				leftButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				leftButton.setIcon(leftButtonBasicImage);
				leftButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				/*Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }*/
				
				//왼쪽 버튼 이벤트
				selectLeft();
			}
		});
		
		add(leftButton);
				

		rightButton.setVisible(false);
		rightButton.setBounds(1030, 310, 100, 100);
		// make button layout clear
		rightButton.setBorderPainted(false);
		rightButton.setContentAreaFilled(false);
		rightButton.setFocusPainted(false);
		rightButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				rightButton.setIcon(rightButtonEnteredImage);
				rightButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				rightButton.setIcon(rightButtonBasicImage);
				rightButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				/*Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }*/
				
				//오른쪽 버튼 이벤트
				selectRight();
			}
		});
		
		add(rightButton);
		
		
		easyButton.setVisible(false);
		easyButton.setBounds(375, 580, 250, 67);
		// make button layout clear
		easyButton.setBorderPainted(false);
		easyButton.setContentAreaFilled(false);
		easyButton.setFocusPainted(false);
		easyButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				easyButton.setIcon(easyButtonEnteredImage);
				easyButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				easyButton.setIcon(easyButtonBasicImage);
				easyButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				/*Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }*/
				
				//난이도 쉬움 이벤트

				gameStart(nowSelected, "Easy");
				
			}
		});
		
		add(easyButton);
		
		
		
		hardButton.setVisible(false);
		hardButton.setBounds(655, 580, 250, 67);
		// make button layout clear
		hardButton.setBorderPainted(false);
		hardButton.setContentAreaFilled(false);
		hardButton.setFocusPainted(false);
		hardButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				hardButton.setIcon(hardButtonEnteredImage);
				hardButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				hardButton.setIcon(hardButtonBasicImage);
				hardButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				/*Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }*/
				
				//난이도 어려움 이벤트
				gameStart(nowSelected, "Hard");
				
				
			}
		});
		
		add(hardButton);
		
		
		backButton.setVisible(false);
		backButton.setBounds(20, 50, 100, 100);
		// make button layout clear
		backButton.setBorderPainted(false);
		backButton.setContentAreaFilled(false);
		backButton.setFocusPainted(false);
		backButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				backButton.setIcon(backButtonEnteredImage);
				backButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				backButton.setIcon(backButtonBasicImage);
				backButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				/*Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }*/
				
				//메인 화면 돌아가는 이벤트
				backMain();
				
			}
		});
		
		add(backButton);
		
		
		
		
		
		infoButton.setVisible(false);
		infoButton.setBounds(1100, 600, 50, 50);
		// make button layout clear
		infoButton.setBorderPainted(false);
		infoButton.setContentAreaFilled(false);
		infoButton.setFocusPainted(false);
		infoButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				infoButton.setIcon(infoButtonEnteredImage);
				infoButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				infoButton.setIcon(infoButtonBasicImage);
				infoButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }
				
				
				//info
				 enterInfo();
			}
		});
		
		add(infoButton);
		
		
		
		infoBackButton.setVisible(false);
		infoBackButton.setBounds(40, 600, 50, 50);
		// make button layout clear
		infoBackButton.setBorderPainted(false);
		infoBackButton.setContentAreaFilled(false);
		infoBackButton.setFocusPainted(false);
		infoBackButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				infoBackButton.setIcon(infoBackButtonEnteredImage);
				infoBackButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				infoBackButton.setIcon(infoBackButtonBasicImage);
				infoBackButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }
				
				
				//backMain
				 backMain();
				 
			}
		});
		
		add(infoBackButton);
		
		
		
		
		
		
		
		scoreS.setVisible(false);
		scoreS.setBounds(0, 30, 1280, 720);
		scoreS.setBorderPainted(false);
		scoreS.setContentAreaFilled(false);
		scoreS.setFocusPainted(false);		
		add(scoreS);
		
		scoreA.setVisible(false);
		scoreA.setBounds(0, 30, 1280, 720);
		// make button layout clear
		scoreA.setBorderPainted(false);
		scoreA.setContentAreaFilled(false);
		scoreA.setFocusPainted(false);		
		add(scoreA);
		
		scoreB.setVisible(false);
		scoreB.setBounds(0, 30, 1280, 720);
		// make button layout clear
		scoreB.setBorderPainted(false);
		scoreB.setContentAreaFilled(false);
		scoreB.setFocusPainted(false);		
		add(scoreB);
		
		scoreC.setVisible(false);
		scoreC.setBounds(0, 30, 1280, 720);
		// make button layout clear
		scoreC.setBorderPainted(false);
		scoreC.setContentAreaFilled(false);
		scoreC.setFocusPainted(false);		
		add(scoreC);
		
		
		

		scoreButton.setVisible(false);
		scoreButton.setBounds(700, 680, 100, 30);
		// make button layout clear
		scoreButton.setBorderPainted(false);
		scoreButton.setContentAreaFilled(false);
		scoreButton.setFocusPainted(false);
		scoreButton.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseEntered(MouseEvent e) {
				scoreButton.setIcon(scoreButtonEnteredImage);
				scoreButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
				Music buttonEnteredMusic = new Music("buttonEnteredMusic.mp3",false);
				buttonEnteredMusic.start();
			}
			
			@Override
			public void mouseExited(MouseEvent e) {
				scoreButton.setIcon(scoreButtonBasicImage);
				scoreButton.setCursor(new Cursor(Cursor.DEFAULT_CURSOR));
			}
			
			@Override
			public void mousePressed(MouseEvent e) {
				/*Music buttonEnteredMusic = new Music("buttonPressedMusic.mp3",false);
				buttonEnteredMusic.start();
				 try {
				 Thread.sleep(1000);
				 } catch (InterruptedException ex) {
				 	ex.printStackTrace();
				 }*/
				
				//점수 화면 돌아가는 이벤트
				if (game.isMusicEnd())
				{
					showScore();
					//
				}
				
				
			}
		});
		
		add(scoreButton);
		
		
		
		
		
		
		

		menuBar.setBounds(0, 0, 1280, 30);
		menuBar.addMouseListener(new MouseAdapter() {
			@Override
			public void mousePressed(MouseEvent e) {
				mouseX = e.getX();
				mouseY = e.getY();
			}
		});
		menuBar.addMouseMotionListener(new MouseMotionAdapter() {
			@Override
			public void mouseDragged(MouseEvent e) {
				int x = e.getXOnScreen();
				int y = e.getYOnScreen();
				setLocation(x-mouseX, y-mouseY);
			}
		});
		add(menuBar);

		while (!game.isMusicEnd())
		{
			System.out.println("Music progressing..");
		}
		scoreButton.setVisible(true);	
		
		
		
		
	}

	public void paint(Graphics g) { // 약속된 메서드
		// create image
		screenImage = createImage(Main.SCREEN_WIDTH, Main.SCREEN_HEIGHT);
		screenGraphic = screenImage.getGraphics();
		// draw image
		screenDraw((Graphics2D)screenGraphic);
		g.drawImage(screenImage, 0, 0, null);
	}

	public void screenDraw(Graphics2D g) {
		g.drawImage(background, 0, 0, null); // draw for background
		if(isMainScreen)
		{
			g.drawImage(selectedImage, 335, 100, null);
			g.drawImage(titleImage, 335, 55, null);
		}
		if(isGameScreen)
		{
			game.screenDraw(g);
		}
		
		paintComponents(g); // draw for Jlabel
		try {
			Thread.sleep(5);
		} catch (Exception e) {
			e.printStackTrace();
		}
		this.repaint(); // call paint function again
		// double buffering technique
	}
	
	
	public void selectTrack(int nowSelected) {
		if(selectedMusic != null)
			selectedMusic.close();
		titleImage = new ImageIcon(Main.class.getResource("../images/" + trackList.get(nowSelected).getTitleImage()))
				.getImage();
		selectedImage = new ImageIcon(Main.class.getResource("../images/" + trackList.get(nowSelected).getStartImage()))
				.getImage();
		selectedMusic = new Music(trackList.get(nowSelected).getStartMusic(),true);
		selectedMusic.start();
	}
	
	
	public void selectLeft() {
		if(nowSelected == 0)
			nowSelected = trackList.size() -1;
		else
			nowSelected--;
		selectTrack(nowSelected);
	}
	
	public void selectRight() {
		if(nowSelected == trackList.size() -1)
			nowSelected = 0;
		else
			nowSelected++;
		selectTrack(nowSelected);
	}
	
	
	public void gameStart(int nowSelected, String difficulty) {
		if(selectedMusic != null)
			selectedMusic.close();
		isMainScreen = false;
		leftButton.setVisible(false);
		rightButton.setVisible(false);
		easyButton.setVisible(false);
		hardButton.setVisible(false);
		background = new ImageIcon(Main.class.getResource("../images/" + trackList.get(nowSelected).getGameImage()))
				.getImage();
		backButton.setVisible(true);
		scoreButton.setVisible(true);
		infoButton.setVisible(false);
		
		isGameScreen = true;
		
		game = new Game(trackList.get(nowSelected).getTitleName(), difficulty, trackList.get(nowSelected).getGameMusic());
		game.start();
		setFocusable(true);
		requestFocus();
			
		
		
	}
	
	public void backMain() {
		isMainScreen = true;
		leftButton.setVisible(true);
		rightButton.setVisible(true);
		easyButton.setVisible(true);
		hardButton.setVisible(true);
		background = new ImageIcon(Main.class.getResource("../images/mainBackground.jpg"))
				.getImage();
		backButton.setVisible(false);
		infoButton.setVisible(true);
		infoBackButton.setVisible(false);
		scoreS.setVisible(false);
		scoreA.setVisible(false);
		scoreB.setVisible(false);
		scoreC.setVisible(false);
		scoreButton.setVisible(false);
		selectTrack(nowSelected);
		isGameScreen = false;
		game.close();
		
	}
	
	public void enterMain() {
		
		startButton.setVisible(false);
		quitButton.setVisible(false);
		background = new ImageIcon(Main.class.getResource("../images/mainBackground.jpg"))
				.getImage();
		isMainScreen = true;
		leftButton.setVisible(true);
		rightButton.setVisible(true);
		easyButton.setVisible(true);
		hardButton.setVisible(true);
		infoButton.setVisible(true);
		
		introMusic.close();
		
		selectTrack(0);
	}
	
	public void enterInfo() {
		
		startButton.setVisible(false);
		quitButton.setVisible(false);
		background = new ImageIcon(Main.class.getResource("../images/mainBackground.jpg"))
				.getImage();
		isMainScreen = false;	
		infoBackButton.setVisible(true);
		infoButton.setVisible(false);
		leftButton.setVisible(false);
		rightButton.setVisible(false);
		easyButton.setVisible(false);
		hardButton.setVisible(false);
		
		
	}
	
	
	public void showScore() {
	
		if(game.getScore() == "S")
		{
			scoreS.setVisible(true);
		}
		else if(game.getScore() == "A")
		{
			scoreA.setVisible(true);
		}
		else if(game.getScore() == "B")
		{
			scoreB.setVisible(true);
		}
		else if(game.getScore() == "C")
		{
			scoreC.setVisible(true);
		}		
		
	}
	
}







Beat.java


package dynamic_beat_17_스코어;

public class Beat {

	private int time;
	private String noteName;
	
	public int getTime() {
		return time;
	}
	public void setTime(int time) {
		this.time = time;
	}
	public String getNoteName() {
		return noteName;
	}
	public void setNoteName(String noteName) {
		this.noteName = noteName;
	}
	public Beat(int time, String noteName) {
		super();
		this.time = time;
		this.noteName = noteName;
	}
	
}








Game.java




package dynamic_beat_17_스코어;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;
import java.io.BufferedReader;
import java.io.FileReader;
import java.util.ArrayList;

import javax.swing.ImageIcon;

public class Game extends Thread {
	
	
	//노트 찍기 연습
	private boolean gameMaker = true; // 제작모드
	
	private boolean musicEnd = false;
	
	
	
	private Image noteRouteLineImage = new ImageIcon(Main.class.getResource("../images/noteRouteLine.png")).getImage();
	private Image judgementLineImage = new ImageIcon(Main.class.getResource("../images/judgementLine.png")).getImage();
	private Image gameInfoImage = new ImageIcon(Main.class.getResource("../images/gameInfo.png")).getImage();	
		
	private Image noteRouteSImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteDImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteFImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteSpace1Image = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteSpace2Image = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteJImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteKImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image noteRouteLImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
	private Image blueFlareImage;
	private Image judgeImage;
	private Image keyPadSImage= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadDImage= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadFImage= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadSpace1Image= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadSpace2Image= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadJImage= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadKImage= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
	private Image keyPadLImage= new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	
	
	
	
	
	private String titleName;
	private String difficulty;
	private String musicTitle;
	private Music gameMusic;
	private int theInt = 0;
	private String scoreDetermined;
	
	ArrayList<Note> noteList = new ArrayList<Note>();
	
	public Game(String titleName, String difficulty, String musicTitle) {
		this.titleName = titleName;
		this.difficulty = difficulty;
		this.musicTitle = musicTitle;
		gameMusic = new Music(this.musicTitle, false);
		
	
	}
	
	public void screenDraw(Graphics2D g) {
		
		g.drawImage(noteRouteSImage, 228, 30, null);
		g.drawImage(noteRouteDImage, 332, 30, null);
		g.drawImage(noteRouteFImage, 436, 30, null);
		g.drawImage(noteRouteSpace1Image, 540, 30, null);
		g.drawImage(noteRouteSpace2Image, 640, 30, null);
		g.drawImage(noteRouteJImage, 744, 30, null);
		g.drawImage(noteRouteKImage, 848, 30, null);
		g.drawImage(noteRouteLImage, 952, 30, null);
		
		g.drawImage(noteRouteLineImage, 224, 30, null);
		g.drawImage(noteRouteLineImage, 328, 30, null);
		g.drawImage(noteRouteLineImage, 432, 30, null);
		g.drawImage(noteRouteLineImage, 536, 30, null);
		g.drawImage(noteRouteLineImage, 740, 30, null);
		g.drawImage(noteRouteLineImage, 844, 30, null);
		g.drawImage(noteRouteLineImage, 948, 30, null);
		g.drawImage(noteRouteLineImage, 1052, 30, null);
				
		g.drawImage(gameInfoImage, 0, 660, null);
		g.drawImage(judgementLineImage, 0, 580, null);
				
		// 노트 눈에 보이게 출력
		for (int i=0; i<noteList.size(); i++)
		{
			Note note = noteList.get(i);
			if(note.getY() > 620)
			{
				judgeImage = new ImageIcon(Main.class.getResource("../images/judgeMiss.png")).getImage();
			}
			if(!note.isProceeded()) {
				noteList.remove(i);
				i--;
			}
			else {
				note.screenDraw(g);
			}
			
		}
		
		
		g.setColor(Color.white);
		// 글자 깨짐 방지
		g.setRenderingHint(RenderingHints.KEY_TEXT_ANTIALIASING, RenderingHints.VALUE_TEXT_ANTIALIAS_ON);
		g.setColor(Color.WHITE);
		g.setFont(new Font("Arial", Font.BOLD, 30));
		g.drawString(titleName, 20, 702);
		g.drawString(difficulty, 1190, 702);
		g.setFont(new Font("Arial", Font.PLAIN, 26));
		g.setColor(Color.DARK_GRAY);
		//Key
		g.drawString("S", 270, 609);
		g.drawString("D", 374, 609);
		g.drawString("F", 478, 609);
		g.drawString("Space Bar", 580, 609);
		g.drawString("J", 784, 609);
		g.drawString("K", 889, 609);
		g.drawString("L", 993, 609);
		g.setColor(Color.LIGHT_GRAY);
		g.setFont(new Font("Elephant", Font.BOLD, 30));
		g.drawString(String.valueOf(theInt), 565, 702);
		g.drawImage(blueFlareImage, 450, 370, null);
		g.drawImage(judgeImage, 460, 420, null);
		g.drawImage(keyPadSImage, 228, 580, null);
		g.drawImage(keyPadDImage, 332, 580, null);
		g.drawImage(keyPadFImage, 436, 580, null);
		g.drawImage(keyPadSpace1Image, 540, 580, null);
		g.drawImage(keyPadSpace2Image, 640, 580, null);
		g.drawImage(keyPadJImage, 748, 580, null);
		g.drawImage(keyPadKImage, 848, 580, null);
		g.drawImage(keyPadLImage, 952, 580, null);
		
		
	}
	
	
	char quotes = '"';
	
	public void pressS() {			
		judge("S");
		noteRouteSImage = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadSImage = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();

		//new Music("스페이스.mp3", false).start();	
		// 제작모드
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "S" + quotes + "),");
		}	
	}	
	public void releaseS() {
		noteRouteSImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadSImage = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	public void pressD() {
		judge("D");
		noteRouteDImage = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadDImage = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();

		//new Music("스페이스.mp3", false).start();
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "D" + quotes + "),");
		}
	}	
	public void releaseD() {
		noteRouteDImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadDImage = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	public void pressF() {
		judge("F");
		noteRouteFImage = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadFImage = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();

		//new Music("스페이스.mp3", false).start();
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "F" + quotes + "),");
		}
	}	
	public void releaseF() {
		noteRouteFImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadFImage = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	public void pressSpace() {
		judge("Space");
		noteRouteSpace1Image = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		noteRouteSpace2Image = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadSpace1Image = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();
		keyPadSpace2Image = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();
		
		//new Music("스페이스.mp3", false).start();
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "Space" + quotes + "),");
		}
	}	
	public void releaseSpace() {
		noteRouteSpace1Image = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		noteRouteSpace2Image = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadSpace1Image = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();
		keyPadSpace2Image = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	public void pressJ() {
		judge("J");
		noteRouteJImage = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadJImage = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();

		//new Music("스페이스.mp3", false).start();
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "J" + quotes + "),");
		}
	}	
	public void releaseJ() {
		noteRouteJImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadJImage = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	public void pressK() {
		judge("K");
		noteRouteKImage = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadKImage = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();

		//new Music("스페이스.mp3", false).start();
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "K" + quotes + "),");
		}
	}	
	public void releaseK() {
		noteRouteKImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadKImage = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	public void pressL() {
		judge("L");
		noteRouteLImage = new ImageIcon(Main.class.getResource("../images/noteRoutePressed.png")).getImage();
		keyPadLImage = new ImageIcon(Main.class.getResource("../images/keyPadPressed.png")).getImage();

		//new Music("스페이스.mp3", false).start();
		if (gameMaker == true)
		{
			System.out.println("new Beat(" + (gameMusic.getTime() - 4080) + ", " + quotes + "L" + quotes + "),");
		}
	}	
	public void releaseL() {
		noteRouteLImage = new ImageIcon(Main.class.getResource("../images/noteRoute.png")).getImage();
		keyPadLImage = new ImageIcon(Main.class.getResource("../images/keyPadBasic.png")).getImage();

	}
	
	@Override
	public void run() {
		dropNotes(this.titleName);
	}
	
	public void close() {
		gameMusic.close();
		this.interrupt();
	}
	
	
	
	public void dropNotes(String titleName) {
		Beat[] beats = null;
		if(titleName.equals("Wild World") && difficulty.equals("Easy")) {
	
			//int startTime = 4460 - Main.REACH_TIME * 1000;
			int gap = 125;
			beats = new Beat[] {
	

					
			};
		}
		else if(titleName.equals("Wild World") && difficulty.equals("Hard")) {
			int startTime = 1000;
			beats = new Beat[] {
					new Beat(startTime, "Space"),
			};
		}
		
		else if(titleName.equals("Temple of Time") && difficulty.equals("Easy")) {
			//int startTime = 1000;
			beats = new Beat[] {
					
			};
		}
		else if(titleName.equals("Temple of Time") && difficulty.equals("Hard")) {
			int startTime = 1000;
			beats = new Beat[] {
					new Beat(startTime, "Space"),
			};
		}
		else if(titleName.equals("The Cygnus Garden") && difficulty.equals("Easy")) {
			int startTime = 1000;
			beats = new Beat[] {
					
					
			};
		}
		else if(titleName.equals("The Cygnus Garden") && difficulty.equals("Hard")) {
			int startTime = 1000;
			beats = new Beat[] {
					
			};
		}
		
		else if(titleName.equals("Shattered Time") && difficulty.equals("Easy")) {
			int startTime = 1000;
			beats = new Beat[] {
					
					

					
					
			};
		}
		else if(titleName.equals("Shattered Time") && difficulty.equals("Hard")) {
			int startTime = 1000;
			beats = new Beat[] {
					
			};
		}
		
		else if(titleName.equals("The Tune of The Azure Light") && difficulty.equals("Easy")) {
			int startTime = 1000;
			beats = new Beat[] {
					
					
			};
		}
		else if(titleName.equals("The Tune of the Azure Light") && difficulty.equals("Hard")) {
			int startTime = 1000;
			beats = new Beat[] {
					
			};
		}
		else if(titleName.equals("Kamado Tanjiro No Uta") && difficulty.equals("Easy")) {
			int startTime = 1000;
			beats = new Beat[] {
					
					
					
			};
		}
		else if(titleName.equals("Kamado Tanjiro No Uta") && difficulty.equals("Hard")) {
			int startTime = 1000;
			beats = new Beat[] {
					
			};
		}
		
		
		
		int i = 0;
		gameMusic.start();
		
		while(i < beats.length && !isInterrupted()) {
			boolean dropped = false;
			
			if(beats[i].getTime() <= gameMusic.getTime()) {
				//System.out.println("Music Start");
				Note note = new Note(beats[i].getNoteName());
				note.start();
				noteList.add(note);
				i++;
				dropped = true;
				
			}
			////////////
			/*else
			{
				System.out.println("Music End");
				musicEnd = true;
			}*/
			if(!dropped) {
				try {
					Thread.sleep(5);
					
				} catch (Exception e) {
					e.printStackTrace();
					
				}
			}
		}
		System.out.println("Music End");
		musicEnd = true;
		
		assignScore();
		
	}
	
	public void judge(String input) {
		for(int i=0; i<noteList.size(); i++)
		{
			Note note = noteList.get(i);
			if(input.equals(note.getNoteType())) {
				judgeEvent(note.judge());
				break;
			}
		}
	}
	
	
	public void judgeEvent(String judge) {
		if(!judge.equals("None")) {
			blueFlareImage = new ImageIcon(Main.class.getResource("../images/blueFlare.png")).getImage();
		}
		if(judge.equals("Miss")) {
			judgeImage = new ImageIcon(Main.class.getResource("../images/judgeMiss.png")).getImage();
		}
		else if(judge.equals("Late")) {
			judgeImage = new ImageIcon(Main.class.getResource("../images/judgeLate.png")).getImage();
			theInt += 30;
		}
		else if(judge.equals("Good")) {
			judgeImage = new ImageIcon(Main.class.getResource("../images/judgeGood.png")).getImage();
			theInt += 100;
		}
		else if(judge.equals("Great")) {
			judgeImage = new ImageIcon(Main.class.getResource("../images/judgeGreat.png")).getImage();
			theInt += 200;
		}
		else if(judge.equals("Perfect")) {
			judgeImage = new ImageIcon(Main.class.getResource("../images/judgePerfect.png")).getImage();
			theInt += 300;
		}
		else if(judge.equals("Early")) {
			judgeImage = new ImageIcon(Main.class.getResource("../images/judgeEarly.png")).getImage();
			theInt += 30;
		}
	}
	
	public boolean isMusicEnd() {
		return this.musicEnd;
	}
	
	public String getScore() {
		return this.scoreDetermined;
	}
	
	
	public void assignScore() {
		if(titleName.equals("Spring") && difficulty.equals("Easy"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Spring") && difficulty.equals("Hard"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Lemon Cake - daystar") && difficulty.equals("Easy"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Lemon Cake - daystar") && difficulty.equals("Hard"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Energy-Bensound") && difficulty.equals("Easy"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Energy-Bensound") && difficulty.equals("Hard"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Memory of Kritias") && difficulty.equals("Easy"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("Memory of Kritias") && difficulty.equals("Hard"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("The Shattered Time") && difficulty.equals("Easy"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("The Shattered Time") && difficulty.equals("Hard"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("The Tune of the Azure Light") && difficulty.equals("Easy"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		else if(titleName.equals("The Tune of the Azure Light") && difficulty.equals("Hard"))
		{
			if(theInt >= 3000)
			{
				scoreDetermined = "S";
			}
			else if(theInt >=2000)
			{
				scoreDetermined = "A";
			}
			else if(theInt >= 1000)
			{
				scoreDetermined = "B";
			}
			else
			{
				scoreDetermined = "C";
			}
		}
		
		
	}
}





KeyListener.java


package dynamic_beat_17_스코어;

import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;

public class KeyListener extends KeyAdapter {
	
	@Override
	public void keyPressed(KeyEvent e) {
		if(DynamicBeat.game == null) {
			return;
		}
		if(e.getKeyCode() == KeyEvent.VK_S) {
			DynamicBeat.game.pressS();			
		}
		else if(e.getKeyCode() == KeyEvent.VK_D) {
			DynamicBeat.game.pressD();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_F) {
			DynamicBeat.game.pressF();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_SPACE) {
			DynamicBeat.game.pressSpace();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_J) {
			DynamicBeat.game.pressJ();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_K) {
			DynamicBeat.game.pressK();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_L) {
			DynamicBeat.game.pressL();	
		}
		
	}
	
	@Override
	public void keyReleased(KeyEvent e) {
		if(DynamicBeat.game == null) {
			return;
		}
		if(e.getKeyCode() == KeyEvent.VK_S) {
			DynamicBeat.game.releaseS();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_D) {
			DynamicBeat.game.releaseD();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_F) {
			DynamicBeat.game.releaseF();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_SPACE) {
			DynamicBeat.game.releaseSpace();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_J) {
			DynamicBeat.game.releaseJ();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_K) {
			DynamicBeat.game.releaseK();	
		}
		else if(e.getKeyCode() == KeyEvent.VK_L) {
			DynamicBeat.game.releaseL();	
		}
		
	}

}







Main.java

package dynamic_beat_17_스코어;

public class Main {
	
	public static final int SCREEN_WIDTH = 1280; // constant -> capital letter
	public static final int SCREEN_HEIGHT = 720;
	public static final int NOTE_SPEED = 8;
	public static final int SLEEP_TIME = 10;
	public static final int REACH_TIME = 2;
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new DynamicBeat();

		
	}

}






Music.java




package dynamic_beat_17_스코어;

import java.io.BufferedInputStream;
import java.io.File;
import java.io.FileInputStream;

import javazoom.jl.player.Player;

public class Music extends Thread {
	
	private Player player;
	private boolean isLoop; // 무한반복, 한번재생 후 끝?
	private File file;
	private FileInputStream fis;
	private BufferedInputStream bis;
	
	public Music(String name, boolean isLoop) {
		try { // set condition
			this.isLoop = isLoop;
			file = new File(Main.class.getResource("../music/" + name).toURI());
			fis = new FileInputStream(file);
			bis = new BufferedInputStream(fis);
			player = new Player(bis);
		} catch (Exception e) {
			System.out.println(e.getMessage());
		}
	}

	// inform where the music is played
	public int getTime() {
		if (player == null)
			return 0;
		return player.getPosition();
	}
	
	// stop music playing (유저가 중간에 다른 곡을 누를때)
	public void close() {
		isLoop = false;
		player.close();
		this.interrupt();
	}
	
	// @override
	public void run() {
		try {
			do {
				player.play();
				fis = new FileInputStream(file);
				bis = new BufferedInputStream(fis);
				player = new Player(bis);
			} while (isLoop);
		} catch (Exception e) {
				System.out.println(e.getMessage());
				
			}
		}
	
}








Note.java



package dynamic_beat_17_스코어;

import java.awt.Graphics2D;
import java.awt.Image;

import javax.swing.ImageIcon;

public class Note extends Thread {
	
	private Image noteBasicImage = new ImageIcon(Main.class.getResource("../images/noteBasic.png")).getImage();
	private int x, y = 580 - (1000/ Main.SLEEP_TIME * Main.NOTE_SPEED) * Main.REACH_TIME;
	private String noteType;
	private boolean proceeded = true;
	
	public String getNoteType() {
		return noteType;
	}
	
	public boolean isProceeded() {
		return proceeded;
	}
	
	public void close() {
		proceeded = false;
	}
	
	public Note(String noteType ) {
		if(noteType.equals("S")) {
			x = 228;
		}
		else if(noteType.equals("D")) {
			x = 332;
		}
		else if(noteType.equals("F")) {
			x = 436;
		}
		else if(noteType.equals("Space")) {
			x = 540;
		}
		else if(noteType.equals("J")) {
			x = 744;
		}
		else if(noteType.equals("K")) {
			x = 848;
		}
		else if(noteType.equals("L")) {
			x = 952;
		}
		this.noteType = noteType;
	}
	
	public void screenDraw(Graphics2D g) {
		if(!noteType.equals("Space"))
		{
			g.drawImage(noteBasicImage, x, y, null);
		}
		else if(noteType.equals("Space"))
		{
			g.drawImage(noteBasicImage, x, y, null);
			g.drawImage(noteBasicImage, x + 100, y, null);
		}
	}
	
	public void drop() {
		y += Main.NOTE_SPEED;
		if (y > 620) {
			//System.out.println("Miss");
			close();
		}
	}
	
	@Override
	public void run() {
		try {
			while (true) {
				drop();
				if(proceeded) {
					Thread.sleep(Main.SLEEP_TIME);
				}
				else {
					interrupt();
					break;
				}
				Thread.sleep(Main.SLEEP_TIME);
			}
			
		} catch(Exception e) {
			System.err.println(e.getMessage());
		}
	}
	public String judge() {
		if(y >= 613)
		{
			//System.out.println("Late");
			close();
			return "Late";
		}
		else if(y >= 600)
		{
			//System.out.println("Good");
			close();
			return "Good";
		}
		else if(y >= 587)
		{
			//System.out.println("Great");
			close();
			return "Great";
		}
		else if(y >= 573)
		{
			//System.out.println("Perfect");
			close();
			return "Perfect";
		}
		else if(y >= 565)
		{
			//System.out.println("Great");
			close();
			return "Great";
		}
		else if(y >= 550)
		{
			//System.out.println("Good");
			close();
			return "Good";
		}
		else if(y >= 535)
		{
			//System.out.println("Early");
			close();
			return "Early";
		}
		return "None";
		
	}
	
	public int getY() {
		return y;
	}
}











Track.java



package dynamic_beat_17_스코어;

public class Track {

	private String titleImage; // 제목 부분 이미지
	private String startImage; // 게임 선택 창 표지 이미지
	private String gameImage; // 해당 곡을 실행했을 때 표지 이미지
	private String startMusic; // 게임 선택 창 음악
	private String gameMusic; // 해당 곡을 실행했을 때 음악
	private String titleName; // 곡 제목
	
	public String getTitleImage() {
		return titleImage;
	}
	public void setTitleImage(String titleImage) {
		this.titleImage = titleImage;
	}
	public String getStartImage() {
		return startImage;
	}
	public void setStartImage(String startImage) {
		this.startImage = startImage;
	}
	public String getGameImage() {
		return gameImage;
	}
	public void setGameImage(String gameImage) {
		this.gameImage = gameImage;
	}
	public String getStartMusic() {
		return startMusic;
	}
	public void setStartMusic(String startMusic) {
		this.startMusic = startMusic;
	}
	public String getGameMusic() {
		return gameMusic;
	}
	public void setGameMusic(String gameMusic) {
		this.gameMusic = gameMusic;
	}
	
	public String getTitleName() {
		return titleName;
	}
	public void setTitleName(String titleName) {
		this.titleName = titleName;
	}
	
	public Track(String titleImage, String startImage, String gameImage, String startMusic, String gameMusic, String titleName) {
		super();
		this.titleImage = titleImage;
		this.startImage = startImage;
		this.gameImage = gameImage;
		this.startMusic = startMusic;
		this.gameMusic = gameMusic;
		this.titleName = titleName;
	}
	
	
	
	
}


