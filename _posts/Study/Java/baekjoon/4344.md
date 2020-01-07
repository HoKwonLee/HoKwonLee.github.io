
**백준 문제 4344번**

**문제**<br>
대학생 새내기들의 90%는 자신이 반에서 평균은 넘는다고 생각한다. 당신은 그들에게 슬픈 진실을 알려줘야 한다.

**입력**<br>
첫째 줄에는 테스트 케이스의 개수 C가 주어진다.<br><br>

둘째 줄부터 각 테스트 케이스마다 학생의 수 N(1 ≤ N ≤ 1000, N은 정수)이 첫 수로 주어지고, 이어서 N명의 점수가 주어진다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.

**출력**<br>
각 케이스마다 한 줄씩 평균을 넘는 학생들의 비율을 반올림하여 소수점 셋째 자리까지 출력한다.

**예제 입력 1** 
```
5
5 50 50 70 80 100
7 100 95 90 80 70 60 50
3 70 90 80
3 70 90 81
9 100 99 98 97 96 95 94 93 91
```
**예제 출력 1**
```
40.000%
57.143%
33.333%
66.667%
55.556%
```

**출처**<br>
Contest > Waterloo's local Programming Contests > 28 September, 2002 D번<br><br>

문제를 번역한 사람: busyhuman<br>
문제의 오타를 찾은 사람: choiking10 eric00513<br>
어색한 표현을 찾은 사람: djm03178<br>

**링크**<br>
PKU Judge Online<br>
ZJU Online Judge<br>
TJU Online Judge<br>

**java code**

```java
import java.util.Scanner;

public class Main {
	
	static class Average{
		
		private int N; //학생수
		private int[] score; //케이스의 학생들
		
		public Average() {
			
		}
		
		public Average(Scanner sc) {
			N = sc.nextInt();
			
			score = new int[N];
			
			for(int n = N - 1; n >= 0; n--) {
				score[n] = sc.nextInt();
			}
		}
		
		float average() {
			int sum = 0;
			
			for(int n = N-1; n >= 0; n--) {
				sum += score[n];
			}
			
			return sum / N;
		}
		
		float OverAvgScore(){
			int count_student = 0;
			
			for(int n = N-1; n >= 0; n--) {
				if(score[n] > average())
					count_student++;
			}
			
			return Math.round((float)count_student / N * 1000 *100) / 1000f;
		}
		
		String tostring() {
			return String.format("%.3f%%",OverAvgScore());
		}
		
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int casenum; //케이스 개수
		
		Scanner sc = new Scanner(System.in);
		
		casenum = sc.nextInt();
		
		Average[] avg = new Average[casenum];
		
		for(int n = casenum; n > 0; n--) {
			avg[n - 1] = new Average(sc);
			sc.nextLine();
		}
		
		for(;casenum>0; casenum--) {
			System.out.println(avg[casenum-1].tostring());
		}
		sc.close();
	}

}
```
