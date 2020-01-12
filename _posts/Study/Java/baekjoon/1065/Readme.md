**백준 문제 1065번 - 한수**<br>

**문제**<br>
어떤 양의 정수 X의 자리수가 등차수열을 이룬다면, 그 수를 한수라고 한다. 등차수열은 연속된 두 개의 수의 차이가 일정한 수열을 말한다. N이 주어졌을 때, 1보다 크거나 같고, N보다 작거나 같은 한수의 개수를 출력하는 프로그램을 작성하시오.<br> 

**입력**<br>
첫째 줄에 1,000보다 작거나 같은 자연수 N이 주어진다.<br>

**출력**<br>
첫째 줄에 1보다 크거나 같고, N보다 작거나 같은 한수의 개수를 출력한다.<br>

------------------------------------------------
**예제 입력 1** 
```
110
```
**예제 출력 1 **
```
99
```
------------------------------------------------
**예제 입력 2**
```
1
```
**예제 출력 2** 
```
1
```
------------------------------------------------
**예제 입력 3 **
```
210
```
**예제 출력 3 **
```
105
```
------------------------------------------------
**예제 입력 4 **
```
1000
```
**예제 출력 4 **
```
144
```
------------------------------------------------
**출처**<br>
문제를 번역한 사람: baekjoon<br>
데이터를 추가한 사람: jh05013<br>
**알고리즘 분류**<br>
브루트 포스<br>
탐색<br>
----------------------------------------
**Java 코드**

```java
import java.io.*;

public class Main {

	public static void main(String[] args) throws NumberFormatException, IOException {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	
		int N = Integer.parseInt(br.readLine());
		int temp;
		int count = 0;
		int digit;
		
		for(int i = 1; i <= N ; i++) {
			digit = (int)Math.log10(i) + 1; //자리수 찾기 
			loop1: 
			switch(digit) {
			case 1: //한 자리이기 때문에 0의 등차로 취급
				count++;
				break;
			case 2: //두 자리이므로 무조건 등차
				count++; 
				break;
			default: //3자리 이상부터는 확인
				temp = i;
				int num[] = new int[digit];
				int AS[] = new int[digit - 1];//Arithmetic Sequence
				for(int j = 0; temp != 0; j++) {
					num[j] = temp % 10;
					if(j > 0)
						AS[j - 1] = num[j] - num[j-1];
					if(j > 1 && AS[j-1] != AS[j-2])
						break loop1;
					temp /= 10;
				}
				count++;
			}
		}
		
		bw.write(count + "");
		
		bw.flush();
		bw.close();
		
	}

}
```
