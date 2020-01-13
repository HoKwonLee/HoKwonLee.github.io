문제
영어 대소문자와 띄어쓰기만으로 이루어진 문자열이 주어진다. 이 문자열에는 몇 개의 단어가 있을까? 이를 구하는 프로그램을 작성하시오. 단, 한 단어가 여러 번 등장하면 등장한 횟수만큼 모두 세어야 한다.

입력
첫 줄에 영어 대소문자와 띄어쓰기로 이루어진 문자열이 주어진다. 이 문자열의 길이는 1,000,000을 넘지 않는다. 단어는 띄어쓰기 한 개로 구분되며, 공백이 연속해서 나오는 경우는 없다. 또한 문자열의 앞과 뒤에는 공백이 있을 수도 있다.

출력
첫째 줄에 단어의 개수를 출력한다.

예제 입력 1 
The Curious Case of Benjamin Button
예제 출력 1 
6
예제 입력 2 
 Mazatneunde Wae Teullyeoyo
예제 출력 2 
3
예제 입력 3 
Teullinika Teullyeotzi 
예제 출력 3 
2
출처
문제를 만든 사람: author5
빠진 조건을 찾은 사람: djm03178 his130
데이터를 추가한 사람: jh05013
내용을 추가한 사람: jh05013
알고리즘 분류
문자열 처리

**Java 코드**
-StringTokenizer 사용 코드

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader (new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter (new OutputStreamWriter(System.out));
		
		StringTokenizer str = new StringTokenizer(br.readLine()," "); 
		int count = 0;
		
		int countTokens = str.countTokens();
		
		for(int i = 0; i < countTokens; i++) {
			count++;
		}
		
		bw.write(count + "");
		
		bw.flush();
		bw.close();
	}

}
```

-StringTokeinzer, split 사용 안한 코드
```java
import java.io.*;

public class Main {

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader (new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter (new OutputStreamWriter(System.out));
		
		int count = 0;
		boolean blank = false;
		
		String str = br.readLine();
		
		//단어인지 확인
		for(int i = 0; i < str.length(); i++) {
			if(blank == false && str.charAt(i) == ' ') {
				blank = true;
			}
			else {
				if(i == 0) {
					count++;
				}
				else if(blank == true) {
					count++;
					blank = false;
				}
			}
		}	
		
		bw.write(count + "");
		
		bw.flush();
		bw.close();
	}

}
```
