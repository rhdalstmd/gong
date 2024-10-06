239p
-----------------------------------------------------
import java.util.Scanner;

public class WordGameApp {
	private Scanner scanner; // 키보드 입력
	private String startWord = "아버지"; // 시작 단어
	private Player[] players; // 게임 참가자들
	
	public WordGameApp() {
		scanner = new Scanner(System.in);	
	}

	// 게임 참가자 수를 입력받고 Player []을 생성하는 메소드
	private void createPlayers() {
		System.out.print("게임에 참가하는 인원은 몇명입니까>>");
		int nPlayers = scanner.nextInt();
		players = new Player[nPlayers]; // Player [] 레퍼런스 배열 생성
		
		// 각 참여자의 이름을 입력받아 Player 객체 생성
		for(int i=0; i<nPlayers; i++) {
			System.out.print("참가자의 이름을 입력하세요>>");
			String name = scanner.next();
			players[i] = new Player(name);
		}		
	}
	
	// lastWord와 참가자가 입력한 newWord를 비교하여 끝말잇기가 잘되었는지 판단
	// 성공하였으면 true 리턴, 아니면 false 리턴
	public boolean checkSuccess(String lastWord, String newWord) {
		int lastIndex = lastWord.length()-1; // 최종 단어의 맨 마지막 문자의 인덱스
		
		// 최종 단어의 맨 마지막 문자와 참가자가 말한 단어의 첫 문자가 같은지 비교
		if(lastWord.charAt(lastIndex) == newWord.charAt(0))
			return true;
		else
			return false;
	}
	
	// 게임을 진행하는 메소드
	public void run() {
		System.out.println("끝말잇기 게임을 시작합니다...");
		createPlayers(); // 참가자를 위한 Player []을 생성한다.
		String lastWord = startWord; // startWord에서 부터 시작한다.

		System.out.println("시작하는 단어는 "+lastWord+ "입니다");
		int next =  0; // 참가자들의 순서대로 증가
		
		// 게임이 끝날 때까지 루프
		while(true) {
			String newWord = players[next].getWordFromUser(); // next 참가자가 단어를 말하도록 한다.
			if(checkSuccess(lastWord, newWord) == false) { // next 참가자가 성공하지 못했다면
				System.out.print(players[next].getName() + "이 졌습니다.");
				break; // 게임을 종료한다.
			}
			next++; // 다음 참가자
			next %= players.length; // next가 참가자의 개수보다 많게 증가하는 것을 막는다.
			lastWord = newWord;
		}
	}
	
	public static void main(String[] args) {
		WordGameApp game = new WordGameApp();
		game.run();
	}
}


// 한 사람의 참가자를 표현하는 클래스
class Player {
	private Scanner scanner; // 키보드 입력
	private String name; // 게임 참가자의 이름
	private String word; // 참가자가 말한 단어
	
	public Player(String name) {
		this.name = name;
		scanner = new Scanner(System.in);	
	}
	
	public String getName() {return name;}
	
	public String getWordFromUser() {
		System.out.print(name+">>");
		word = scanner.next();
		return word;
	}
	
}
------------------------------------------
245p
public class TV {
	private String maker; // 제조사
	private int size; // 크기(단위: 인치)
	private int price; // 가격(단위: 만원)
	
	public TV(String maker, int size, int price) {
		this.maker = maker;
		this.size = size;
		this.price = price;
	}
	
	public void show() {
		System.out.println(maker +"에서 만든 " + price + "만원짜리의 " + size + "인치 TV");
	}
	
	public static void main(String[] args) {
		TV tv = new TV("Samsung", 50, 300); // 300만원짜리 Samsung에서 만든 50인치 TV
		tv.show();		
	}
}
------------------------------------------------------
import java.util.Scanner;

public class Grade {
	private String name; // 학생 이름
	private int java, web, os; // 과목 점수
	
	public Grade(String name, int java, int web, int os) { // 생성자
		this.name = name;
		this.java = java;
		this.web = web;
		this.os = os;
	}
	
	public String getName() { return name; }
	
	public int getAverage() {
		return (java+web+os)/3;
	}
	
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("이름, 자바, 웹프로그래밍, 운영체제 순으로 점수 입력>>");
		String name = scanner.next();
		int java = scanner.nextInt();
		int web = scanner.nextInt();
		int os = scanner.nextInt();
		Grade st = new Grade(name, java, web, os); // 한 명의 점수 객체 생성
		System.out.print(st.getName() + "의 평균은 " + st.getAverage());
		scanner.close();
	}

}
--------------------------------------------------------------------
// 노래 한 곡을 나타내는 클래스
public class Song {
	private String title; // 제목
	private String singer; // 가수
	private int year; // 발표 년도
	private String country; // 나라
	
	public Song(String title, String singer, int year, String country) {
		this.title = title;
		this.singer = singer;
		this.year = year;
		this.country = country;
	}
	
	public void show() {
		System.out.println(year+"년 " + country + "의 " + singer + "가 부른 " + title);
	}
	
	public static void main(String[] args) {
		Song song = new Song("가로수 그늘 아래 서면", "이문세", 1988, "한국");
		song.show();
	}

}
----------------------------------------------------------------------------
public class Memo {
	private String name; // 작성자 이름
	private String time; // 메모를 작성한 시간
	private String content; // 메모 내용

	public boolean isSameName(Memo b) { // 메모 내용 출력
		if(name.equals(b.getName())) return true;
		else return false;
	}

	public String getName() { // 메모 작성자 이름 리턴
		return name;
	}
	
	public int length() { // 메모 텍스트의 길이
		return content.length();
	}

	public void show() { // 메모 내용 출력
		System.out.println(name + ", " + time + " " + content);
	}
	
	public Memo(String name, String time, String content) { // 생성자. 멤버 필드 초기화
		this.name = name;
		this.time = time;
		this.content = content;
	}

	public static void main(String[] args) {
		Memo a = new Memo("유송연", "10:10", "자바 과제 있음");
		Memo b = new Memo("박채원", "10:15", "시카고로 어학 연수가요!");
		Memo c = new Memo("김경미", "11:30", "사랑하는 사람이 생겼어요.");

		a.show();
		if(a.isSameName(b)) System.out.println("동일한 사람입니다.");
		else System.out.println("다른 사람입니다.");
		System.out.println(c.getName() + "가 작성한 메모의 길이는 " + c.length());
	}

}------------------------------------------------------------------
import java.util.Scanner;

class Player {
	private String name;
	private int winnerCount;
	private int lastGuessNumber;
	
	public Player(String name) {
		this.name = name;
		this.winnerCount = 0;
	}
	
	public String getName() { return name; }
	public int getWinnerCount() { return winnerCount; }
	public void addWinnerCount() { winnerCount++; }
	
	public int getGuessNumber() { return lastGuessNumber; }
	public void setGuessNumber(int n) { lastGuessNumber = n; }
	
	public void show() {
		System.out.print(name + ":" + winnerCount);
	}
}

public class GuessGame {
	private String name; // 게임 이름
	private Player [] players = null; // 게임이 참여하는 선수들의 레퍼런스 배열
	private Scanner scanner = new Scanner(System.in);
	
	public GuessGame(String name) { // 생성자에서 게임 이름 전달 받아 저장
		this.name = name;
	}
	
	private void createPlayers() { // 선수들 Player 객체 배열 및 Player 객체들 생성
		System.out.print("게임에 참여할 선수 수>>");
		int n = scanner.nextInt();
		players = new Player [n]; // Player [] 배열 생성
		for(int i=0; i<n; i++) {
			System.out.print("선수 이름>>");
			String name = scanner.next();
			players[i] = new Player(name); // n 명의 선수 객체 생성
		}
		// Players [] 배열 생성 완료
	}
	
	private void doGame() {
		while(true) {
			int hiddenAnswer = (int)(Math.random()*100 + 1);
			System.out.println("1~100사이의 숫자가 결정되었습니다. 선수들은 맞추어 보세요.");
			
			// 각 선들로 부터 예측 수 입력 받기
			for(int i=0; i<players.length; i++) {
				String playerName = players[i].getName();
				System.out.print(playerName + ">>");
				int guessNumber = scanner.nextInt();
				if(guessNumber <= 0 || guessNumber > 100) {
					System.out.println("1~100사이의 숫자만 입력하세요!!");
					i--;
					continue;
				}
				players[i].setGuessNumber(guessNumber);
			}
			
			// 가장 가까운 수를 맞춘 선수 결정
			Player nearestPlayer = decideNearestPlayer(hiddenAnswer);
			
			// 이긴 선수에게 점수 부여
			nearestPlayer.addWinnerCount();
			
			System.out.println("정답은 " + hiddenAnswer + ". " + nearestPlayer.getName() + "이 이겼습니다. 승점 1점 확보!");
			System.out.print("계속하려면 yes 입력>>");
			String res = scanner.next();
			if(res.equals("yes"))
				continue;
			else { // 게임 끝. 누적된 승리 횟수가 많은 사람이 최종 승자
				Player winner = decideWinner();
				printAllWinnerCount(); // 선수별 승리 횟수 모두 출력
				System.out.print(winner.getName() + "이 최종 승리하였습니다.");
				break; // 프로그램 종료
			}
		}
			
	}
	
	// 가장 가까운 수를 맞춘 선수를 결정하여 리턴하는 메소드
	private Player decideNearestPlayer(int hiddenAnswer) {
		Player nearestPlayer = players[0]; // 선수 0 번이 답에 가장 가까운 것으로 초기화
		int nearestDiff = Math.abs(hiddenAnswer -  nearestPlayer.getGuessNumber()); // 선수0번의 답과 정답과의 차이
		for(int i=0; i<players.length; i++) {
			int diff = Math.abs(hiddenAnswer -  players[i].getGuessNumber()); // 선수 i 번의 답과 정답과의 차이
			if(diff < nearestDiff) { // 선수 i 번의 답과 정답과의 차이가 가장 작은 차이보다 더 작을 때
				nearestDiff = diff; // 정답에 가장 가까운 답 사이의 차이를 선수 i 의 차이로 수정
				nearestPlayer = players[i]; // 선수 i가 가장 가까운 답을 제시한 것으로 수정
			}				
		}
		
		return nearestPlayer;
	}
	
	// 최종 승자를 결정하여 리턴하는 메소드
	private Player decideWinner() {
		Player winner = players[0]; // 선수 0 번을 최종 승자로 초기화
		for(int i=0; i<players.length; i++) {
			if(winner.getWinnerCount() < players[i].getWinnerCount())
				winner = players[i];
		}
		
		return winner;
	}
	
	private void printAllWinnerCount() {
		for(int i=0; i<players.length; i++) {
			players[i].show();
			System.out.print(" ");
		}
		System.out.println();
	}
	
	public void run() {
		System.out.println("*** " + name + "을 시작합니다. ***");
		createPlayers();
		doGame();
	}
	
	public static void main(String[] args) {
		GuessGame game = new GuessGame("예측 게임");
		game.run();
	}

}
----------------------------------------------------------------------------
class ArrayUtil {	
	public static int [] concat(int[] a, int[] b) { // 배열 a와 b를 연결한 새로운 배열 리턴
		int tmp [] = new int [a.length + b.length]; // 배열 a와 b를 합한 크기의 배열 생성
		for(int i=0; i<a.length; i++) // 배열 a를 tmp로 복사
			tmp[i] = a[i];

		for(int i=0; i<b.length; i++) { // 배열 b를 tmp로 복사
			int index = a.length + i;
			tmp[index] = b[i];
		}

		return tmp;
	}
	public static void print(int[] a) { // 배열 a 출력
		System.out.print("[ ");
		for(int i=0; i<a.length; i++) {
			System.out.print(a[i] + " ");
		}
		System.out.println("]");
	}
}

public class StaticEx {
	public static void main(String [] args){
		int [] array1 = { 1, 5, 7, 9 };
		int [] array2 = { 3, 6, -1, 100, 77 };
		int [] array3 = ArrayUtil.concat(array1, array2);
		ArrayUtil.print(array3);
	}
}
------------------------------------------------------------------------------
import java.util.Scanner;

public class Concert {
	private String hallName;
	private Group[] group = new Group[3];
	private Scanner scanner = new Scanner(System.in);

	public Concert(String hallName) {
		this.hallName = hallName;
		group[0] = new Group('S', 10); // S 타입 좌석 생성
		group[1] = new Group('A', 10); // A 타입 좌석 생성
		group[2] = new Group('B', 10); // B 타입 좌석 생성 
		
	}
	
	private void reserve() { // 콘서트 예약
		System.out.print("좌석구분 S(1), A(2), B(3)>>");
		int type = scanner.nextInt();
		if (type < 1 || type > 3) {
			System.out.println("잘못된 좌석 타입입니다.");
			return;
		}
		group[type-1].reserve();
		
	}
	
	private void search() { // 콘서트 예약 검색
		for (int i=0;i<group.length; i++)
			group[i].show();
		System.out.println("<<<조회를 완료하였습니다.>>>");		
	}
	
	private void cancel() { // 콘서트 예약 취소
		System.out.print("좌석 S:1, A:2, B:3>>");
		int type = scanner.nextInt();
		if (type < 1 || type > 3) {
			System.out.println("잘못된 좌석 타입입니다.");
			return;
		}
		group[type-1].cancel();
	}
	
	public void run() { // 콘서트 예약/취소/검색 등 
		System.out.println(hallName + " 예약 시스템입니다.");
		int choice = 0;
		while (choice != 4) { 
			System.out.print("예약:1, 조회:2, 취소:3, 끝내기:4>>");
			choice = scanner.nextInt();
			switch (choice) {
				case 1:	// 예약
					reserve();
					break;
				case 2:	// 조회
					search();
					break;
				case 3:	// 취소
					cancel();
					break;
				case 4:	// 끝내기
					break;
				default:
					System.out.println("잘못 입력하셨습니다.");
			}
		}
	}
}
---------------------------------------------------------------------
public class ConcertApp {
	
	public static void main (String[] args) {
		Concert concert = new Concert("명품콘서트홀");
		concert.run();
	}
}
-----------------------------------------------------------------
import java.util.Scanner;

public class Group {
   private char type; // 'S', 'A', 'B' 석을 나타내는 문자 
   private Seat[] seats; // 현재 등급의 좌석 객체 배열
   private Scanner scanner = new Scanner(System.in);
   
   public Group(char type, int num) {
	   this.type = type;
	   seats = new Seat[num];
	   for (int i=0; i<seats.length; i++)
		   seats[i] = new Seat();
   }
   public boolean reserve() { // 현재 등급의 좌석 예약
	   int no;
	   String name;
	   show();
	   System.out.print("이름>>");
	   name = scanner.next();
	   System.out.print("번호>>");
	   no = scanner.nextInt();
	   if (no < 1 || no >= seats.length) {
		   System.out.println("잘못된 좌석번호입니다.");
		   return false;
	   }
	   if (seats[no-1].isOccupied()) { // 이미 예약된 좌석 번호
		   System.out.println("이미 예약된 좌석입니다.");
		   return false;
	   }
	   seats[no-1].reserve(name);
	   return true;
   }
   public boolean cancel() { // 현재 등급의 좌석 취소
	   show();
	   System.out.print("이름>>"); // 취소할 예약자 이름 입력
	   String name = scanner.next();
	   if (name != null) {
		   for (int i=0;i<seats.length; i++) {
			   if (seats[i].match(name)) {
				   seats[i].cancel();
				   return true;
			   }
		   }
		   System.out.println("예약자 이름을 찾을 수 없습니다.");
	   }
	   return false; // 예약자 이름을 찾지 못함
   }
   
   public void show() { // 현재 등급의 좌석 출력
	   System.out.print(type + ">> ");
	   for (int i=0; i<seats.length; i++) {
		   if (seats[i].isOccupied())
			   System.out.print(seats[i].getName());
		   else
			   System.out.print("---");
		   System.out.print(" ");
	   }
	   System.out.println();
   }
}
------------------------------------------------------------------
public class Seat {
   private String name;
   public Seat() {
	   name = null;
   }
   public String getName() {
	   return name;
   }
   public void cancel() {
	   name = null;
   }
   public void reserve(String name) {
	   this.name = name;
   }
   public boolean isOccupied() {
	   if (name == null) // 좌석이 예약되어 있으면 true 반환
		   return false;
	   else 
		   return true;
   }
   public boolean match(String name) {
	   return(name.equals(this.name));
   }
}
