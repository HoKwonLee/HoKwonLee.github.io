**가장 긴 증가하는 부분 수열**

**문제**<br>
수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.<br>

예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.

**입력**<br>
첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.<br>

둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)<br>

**출력**<br>
첫째 줄에 수열 A의 가장 긴 증가하는 부분 수열의 길이를 출력한다.
<br>
**예제 입력 1** 
```
6
10 20 10 30 20 50
```
**예제 출력 1**
```
4
```
**출처**<br>
문제를 만든 사람: baekjoon<br>
데이터를 추가한 사람: harinboy

-------------------------------------------------------------
**java code**

```java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner sc = new Scanner(System.in);
		
		int length;
		int A[];
		int sub[];
		
		length = sc.nextInt();
		
		A = new int[length];
		sub = new int[length];
		
		for(int i = 0; i<length; i++) {
			A[i] = sc.nextInt();
		}
		
		for(int i = 0; i < length; i++) {
			sub[i] = 1;
			for(int j = 0; j < i; j++) {
				if(A[j] < A[i] && sub[i] < sub[j] + 1)
					sub[i] = sub[j] + 1;
			}
		}
		
		int ans = sub[0];
		
		for(int i = 0 ; i < length; i++) {
			if (ans < sub[i]) {
				ans = sub[i];
			}	
		}
		
		System.out.println(ans);
		
		sc.close();
	}

}
```
