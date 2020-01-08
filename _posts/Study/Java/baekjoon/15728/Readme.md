**백준 문제 15728*<br>

**에리 - 카드**<br>

**문제**<br>
2468년 개최된 해왕성 올림픽, ‘에리 - 카드’는 드디어 올림픽 정식 종목으로 채택된다. ‘에리 - 카드’는 N 장의 ‘공유 숫자카드’와 N 장의 ‘팀 숫자카드’를 받고 시작한다. 상대 팀은 우리 팀의 ‘팀 숫자카드’ K 장을 견제할 수 있는데, 견제된 카드는 낼 수 없게 된다. 모든 견제가 마친 후 우리 팀은 ‘공유 숫자카드’에서 한 장, ‘팀 숫자카드’ 중 한 장씩을 골라 내게 되는데, 두 카드의 곱이 우리 팀의 점수가 되며 이후 같은 방식으로 상대 팀도 진행하여 상대 팀의 점수보다 높을 경우 이기게 된다.

상대팀은 항상 최선의 방법으로 N장의 우리 팀의 ‘팀 숫자카드’ 중 K장을 견제한다고 했을 때, 우리 팀이 얻을 수 있는 최대 점수를 출력하는 프로그램을 작성하시오.

**입력**<br>
첫째 줄에 N, K(0 ≤ K < N ≤ 100)가 주어지고 둘째 줄에는 N개의 ‘공유 숫자카드’에 적혀 있는 정수, 셋째 줄에는 N개의 ‘팀 숫자카드’에 적혀 있는 정수가 주어진다. 이 수는 -10,000보다 크거나 같고, 10,000보다 작은 정수이다.

**출력**<br>
우리 팀이 얻을 수 있는 최대 점수를 출력한다.<br>

**예제 입력 1** <br>
```
5 2
-1 2 3 4 5
-1 0 2 3 4
```
**예제 출력 1** <br>
```
10
```
**힌트**<br>
상대팀은 ‘팀 숫자카드’ 2장의 카드를 견제 할 수 있고 가장 큰 점수가 나올 수 있는 카드 4와 카드 3을 견제할 것이다.<br>
이후 남은 카드로 이 팀은 ‘공유 숫자카드’의 카드 5와 ‘팀 숫자카드’의 카드 2로 최대 10점을 얻을 수 있다.<br>

**출처**<br>
University > 한양대 ERICA > 2018 HEPC - MAVEN 4번<br>

문제를 만든 사람: hellogaon<br>
문제의 오타를 찾은 사람: jh05013<br>
잘못된 데이터를 찾은 사람: tncks0121<br>

---------------------------------------------------------
**java 코드**<br>

```java
package a15728;

import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner sc = new Scanner(System.in);
		
		int N = sc.nextInt();//shareCard, teamCard의 갯수
		int K = sc.nextInt();//teaCard 제외 갯수
		
		int shareCard[] = new int[N];//shareCard 배열
		int teamCard[] = new int[N]; //teamCard배열
		int Max[] = new int[N]; //teamCard에 따른 최대값
		int temp;
		
		//Max배열 값 초기화
		for(int i = 0; i < N; i++)
			Max[i] = -99999;
		
		//공유카드, 팀카드 값 채워넣기
		for(int i = 0; i < 2; i++) {
			for(int j = 0; j < N; j++) {
				if(i==0) {
					shareCard[j] = sc.nextInt();
				}
				else {
					teamCard[j] = sc.nextInt();
				}
			}
		}
		
		//teamCard의 값에 따른 최대값 탐색
		for(int i = 0; i < N; i++) {
			for(int j = 0; j < N; j++) {
				temp = shareCard[j] * teamCard[i];
				if(Max[i] < temp)
					Max[i] = temp;
			}
		}
		
		//버블정렬로 Max값 정렬
		for(int i = N-1; i > 0; i--) {
			for(int j = 0; j < i; j++) {
				if(Max[j] < Max[j+1]) {
					int te;
					te = Max[j];
					Max[j] = Max[j+1];
					Max[j+1] = te;
				}
			}
		}
		
		//K+1번째 값 출력
		System.out.println(Max[K]);
		
	}
}

```

**Comment**<br>

처음 생각엔 '공유카드'와 '팀 카드'의 최대값끼리 곱만 비교하면 괜찮겠다 생각을 하였다.<br><br>
그러나 이런 경우엔 음수 x 양수 or 음수 x 음수의 경우는 답이 틀리게 나왔다.<br><br>
그럼 '공유카드' 와 '팀카드'의 최대값과 최소값끼리만 비교하면 되겠지?라고 생각하여<br><br>
**최대값 x 최대값**, **최소값 x 최소값**, **최대값 x 최소값**, **최소값 x 최대값** 4가지 경우를 비교했다.<br><br>
다른 반례를 생각하지 못해서 그냥 완전탐색으로 각 '팀카드'에 따른 최대값 배열을 모두 찾고<br><br>
그 중 K만큼 없앤 값 이후를 출력하기로 했다.<br><br>
시간이 120ms가 걸려 다른 코드들에 비하면 느려서 규칙을 한번 생각해봐야겠다.
