**백준 문제 - 셀프 넘버**<br>

**문제**<br>
셀프 넘버는 1949년 인도 수학자 D.R. Kaprekar가 이름 붙였다. 양의 정수 n에 대해서 d(n)을 n과 n의 각 자리수를 더하는 함수라고 정의하자. 예를 들어, d(75) = 75+7+5 = 87이다.<br>

양의 정수 n이 주어졌을 때, 이 수를 시작해서 n, d(n), d(d(n)), d(d(d(n))), ...과 같은 무한 수열을 만들 수 있다.<br> 

예를 들어, 33으로 시작한다면 다음 수는 33 + 3 + 3 = 39이고, 그 다음 수는 39 + 3 + 9 = 51, 다음 수는 51 + 5 + 1 = 57이다. 이런식으로 다음과 같은 수열을 만들 수 있다.<br>

33, 39, 51, 57, 69, 84, 96, 111, 114, 120, 123, 129, 141, ...<br>

n을 d(n)의 생성자라고 한다. 위의 수열에서 33은 39의 생성자이고, 39는 51의 생성자, 51은 57의 생성자이다. 생성자가 한 개보다 많은 경우도 있다. 예를 들어, 101은 생성자가 2개(91과 100) 있다.<br> 

생성자가 없는 숫자를 셀프 넘버라고 한다. 100보다 작은 셀프 넘버는 총 13개가 있다. 1, 3, 5, 7, 9, 20, 31, 42, 53, 64, 75, 86, 97<br>

10000보다 작거나 같은 셀프 넘버를 한 줄에 하나씩 출력하는 프로그램을 작성하시오.<br>

**입력**<br>
입력은 없다.<br>

**출력**<br>
10,000보다 작거나 같은 셀프 넘버를 한 줄에 하나씩 증가하는 순서로 출력한다.<br>

**예제 출력 1**
```
1
3
5
7
9
20
31
42
53
64
 |
 |       <-- a lot more numbers
 |
9903
9914
9925
9927
9938
9949
9960
9971
9982
9993
```
**출처**<br>
ICPC > Regionals > North America > Mid-Central Regional > 1998 Mid-Central Regional Programming Contest D번<br>

문제를 번역한 사람: baekjoon<br>
문제의 오타를 찾은 사람: eric00513<br>

**링크**<br>
ACM-ICPC Live Archive<br>
PKU Judge Online<br>
ZJU Online Judge<br>
TJU Online Judge<br>
HDU Online Judge<br>
**알고리즘 분류**<br>
에라토스테네스의 체<br>
입문용<br>
**채점**<br>
예제는 채점하지 않는다.

----------------------------------------------
**문제 해결 방법**<br>

우선 **셀프넘버는 생성자가 없는 수**이다.<br>

**d(n)**은 **n + 각 자리의 수**이므로

d(n)에 대한 코드는 아래와 같다
```java
int d(int n){
  int sum = temp = n;
  do {
    sum += temp % 10;
    temp /= 10;
  }while(temp != 0);
  return sum;
}
```
여기에 n이 셀프넘버인지를 확인하는 부분을 추가하여 **boolean형 selfNum 함수**를 만들었다.<br>

----------------------------------------------
**Java 코드**<br>

```java
import java.io.*;

public class Main {

	//d(n)에 해당하는 함수
	static boolean selfNum(int n) {
		int i;
		for(i = n - 1; i > 0; i--) {
			int s = i, temp = i;
			do {
				s += temp % 10;
				temp /= 10;
			}while(temp != 0);
			if(s == n) {
				return false;
			}
		}
		
		return true;
	}

	public static void main(String[] args) throws NumberFormatException, IOException {
		// TODO Auto-generated method stub
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	
		for(int i = 1; i <= 10000; i++) {
			if(selfNum(i) == true)
				bw.write(i+"\n");
		}
		
		bw.flush();
		bw.close();
		
	}

}
```
-------------------------------------------------------------------------
**Comment**<br>

n의 값이 셀프 넘버인지를 찾는 방식은 비효율적으로 찾게 만들었다.
오히려 b(n)의 값들을 전부 찾은뒤 이 값들과 1~10,000이 중복되는지 확인하는 식으로 구현을 했으면
더 효율적으로 만들 수 있을 것 같다.
