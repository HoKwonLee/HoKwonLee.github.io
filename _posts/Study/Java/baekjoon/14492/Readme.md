**백준 문제 14492**<br><br>
**부울행렬의 부울곱**<br><br>

**문제**<br>
문제를 출제하던 욱제는 갑자기 괴랄한 문제를 내고 싶어졌다. 불행하게도, 이번 대회에는 프로그래밍 뉴비들이 많기 때문에 그럴 수는 없었다. 하지만 욱제는 신입생들을 괴롭히고픈 욕망을 포기할 수 없었다.<br>

‘하하! 과연 신입생들이 이 문제를 풀 수 있을까?’<br>

문제는 간단하다. N*N 크기의 두 부울행렬(0과 1로만 이루어진 행렬) A=[aij]와 B=[bij]가 주어졌을 때, 두 행렬에 대해 부울곱 연산을 수행한 행렬 C=[cij]에 나타나는 1의 개수를 세는 것이다. 부울곱 연산은 아래와 같이 수행된다.<br>

cij = (ai1∧b1j)∨(ai2∧b2j)∨...∨(ain∧bnj)<br>

xij는 X행렬의 i행j열 원소를 뜻하며 ∧는 논리곱(AND), ∨는 논리합(OR) 연산을 나타낸다. 자, 어서 코딩하자!<br>

**입력**<br>
첫째 줄에 행렬의 크기 N(1<=N<=300)이 주어진다. 이후 N개의 줄에 N*N의 부울행렬 A=[aij]와, 다음 N개의 줄에 N*N의 부울행렬 B=[bij]가 주어진다.<br>

**출력**
A☉B를 연산한 행렬 C에서 나타나는 1의 개수를 세어서 출력한다.<br>

**예제 입력 1**
```
3
1 1 0
0 1 0
0 0 1
1 0 0
1 1 1
0 0 1
```
**예제 출력 1**
```
7
```
**예제 입력 2**
```
2
0 1
1 1
1 1
0 0
```
**예제 출력 2**
```
2
```
**힌트**<br>
예제1의 연산 결과는 다음과 같다.<br>
```
1 1 1
1 1 1
0 0 1
```
따라서 1의 개수는 7이다.<br>

예제2의 연산 결과는 다음과 같다.
```
0 0
1 1
```
따라서 1의 개수는 2이다.<br>

**출처**<br>
High School > 선린인터넷고등학교 > 2017 선린 봄맞이 교내대회 F번<br>

데이터를 추가한 사람: cubelover<br>
문제를 만든 사람: wookje<br>

---------------------------------------------------------------------------
**Java 코드**<br>

```java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int N;
		int temp;
		int count = 0;
		
		boolean a[][];
		boolean b[][];
		boolean c[][];
		
		Scanner sc = new Scanner(System.in);
		
		N = sc.nextInt();
		
		a = new boolean[N][N];
		b = new boolean[N][N];
		c = new boolean[N][N];
		
		//B[i][j] 행렬 입력
		for(int i = 0; i < N; i++)
			for(int j = 0 ; j < N; j++) {
				temp= sc.nextShort();
				// 0,1이 부울식에 들어갈수 있도록 변경
				if(temp == 0)
					a[i][j] = false;
				else if(temp == 1)
					a[i][j] = true;
				else
					j--;
			}
		
		//B[i][j] 행렬 입력
		for(int i = 0; i < N; i++)
			for(int j = 0 ; j < N; j++) {
				temp= sc.nextShort();
				// 0,1이 부울식에 들어갈수 있도록 변경
				if(temp == 0)
					b[i][j] = false;
				else if(temp == 1)
					b[i][j] = true;
				else
					j--;
			}
		
		//C[i][j] 행렬 값 구하기.
		for(int i = 0; i < N; i++) {
			for(int j = 0; j < N; j++) {
				for(int k = 0; k < N; k++) {
					c[i][j] = c[i][j] || (a[i][k] && b[k][j]);
					//C[i][j]는 SOP구조이므로 true가 되면 뒤에는 확인하지 않아도 된다.
					if(c[i][j] == true) {
						count++;
						break;
					}
				}
			}
		}
		
		System.out.println(count);
		
		sc.close();
	}

}
```

**Comment**<br>
이번껀 java의 경우 C와 다르게 boolean에 0,1이 아닌 true, false가 들어가 0,1을 넣을경우 오류가 생겨 0,1을 입력 받을 시 true, false변경하는 식을 넣어줬다.
