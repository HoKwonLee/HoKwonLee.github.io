---
title: "ID : PICNIC"
date: 2020-01-06 20:39:28 -0400
categories: Java_Algorism
---

**문제 ID : PICNIC**
안드로메다 유치원 익스프레스반에서는 다음 주에 율동공원으로 소풍을 갑니다. 원석 선생님은 소풍 때 학생들을 두 명씩 짝을 지어 행동하게 하려고 합니다. 그런데 서로 친구가 아닌 학생들끼리 짝을 지어 주면 서로 싸우거나 같이 돌아다니지 않기 때문에, 항상 서로 친구인 학생들끼리만 짝을 지어 줘야 합니다.

각 학생들의 쌍에 대해 이들이 서로 친구인지 여부가 주어질 때, 학생들을 짝지어줄 수 있는 방법의 수를 계산하는 프로그램을 작성하세요. 짝이 되는 학생들이 일부만 다르더라도 다른 방법이라고 봅니다. 예를 들어 다음 두 가지 방법은 서로 다른 방법입니다.
```
-(태연,제시카) (써니,티파니) (효연,유리)
-(태연,제시카) (써니,유리) (효연,티파니)
```
**입력**
입력의 첫 줄에는 '<u>테스트 케이스의 수 C (C <= 50)</u>' 가 주어집니다. 각 테스트 케이스의 첫 줄에는 학생의 수 n (2 <= n <= 10) 과 친구 쌍의 수 m (0 <= m <= n*(n-1)/2) 이 주어집니다. 그 다음 줄에 m 개의 정수 쌍으로 서로 친구인 두 학생의 번호가 주어집니다. 번호는 모두 0 부터 n-1 사이의 정수이고, 같은 쌍은 입력에 두 번 주어지지 않습니다. 학생들의 수는 짝수입니다.

**출력**
각 테스트 케이스마다 한 줄에 모든 학생을 친구끼리만 짝지어줄 수 있는 방법의 수를 출력합니다.

**예제 입력**
```
3 
2 1 
0 1 
4 6 
0 1 1 2 2 3 3 0 0 2 1 3 
6 10 
0 1 0 2 1 2 1 3 1 4 2 3 2 4 3 4 3 5 4 5
```
**예제 출력**
```
1
3
4
```

---------------------------------------------------------------------------------------------------------------------------------

**소스코드**

```java
package picnic;

import java.util.Scanner;
import java.util.StringTokenizer;


public class PicnicTest {

	static int N; //학생수 (2<=n<=10)
	static int M; //친구 쌍의 수 (0 <= m <= n(n-1)/2)
	static boolean friends[][]; //친한친구 순서쌍
	
	public static void Picninc() {
		Scanner sc = new Scanner(System.in);
		
		StringTokenizer st = new StringTokenizer(sc.nextLine());
		
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		assert N>2 | N<10 | M>0 | M<((N*(N-1))/2); //학생수, 친구쌍의 수 예외처리
		
		friends = new boolean[N][N];
		StringTokenizer frd = new StringTokenizer(sc.nextLine());
		//친구쌍이 있는지 확인
		while(frd.hasMoreTokens()) {
			int f1 = Integer.parseInt(frd.nextToken()); // (f1,f2) 확인
			int f2 = Integer.parseInt(frd.nextToken());
			assert f1>=0 | f1<N | f2>= 0 | f2<N;
			friends[f1][f2] = friends[f2][f1] = true;
		}
		
		sc.close();
		
		boolean[] bePaired = new boolean[N];
		System.out.println(countPairings(bePaired));
	}
	
	public static int countPairings(boolean[] bePaired) {
		int fastNum = -1;
		for(int i = 0; i < N; i++) {
			if(!bePaired[i]) {
				fastNum = i;
				break;
			}
		}
		
		if(fastNum == -1)
			return 1;
		int ret = 0;
		for(int w=fastNum+1; w<N; w++) {
			if(!bePaired[w] & friends[fastNum][w]) {
				bePaired[fastNum] = bePaired[w] = true;
				ret += countPairings(bePaired);
				bePaired[fastNum] = bePaired[w] = false;
			}
		}
		return ret;
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		Picninc();
	}


}
```
---------------------------------------------------------------------------------------------------------------------------------
