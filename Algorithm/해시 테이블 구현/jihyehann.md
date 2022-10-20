# 💡 해시 테이블 구현

> 이전에 정리했던 [해시 자료구조](https://github.com/jaejlf/CS_Study/blob/main/Data%20Structure/%ED%95%B4%EC%8B%9C(Hash)/jihyehann.md)를 먼저 보고 오자.

다시 정리하면, 해시 테이블은 탐색을 최대한 줄여주기 위해, input에 대한 key 값을 얻어내서 관리하는 방식이다.

완전 탐색 알고리즘으로 문제를 풀었을 때, 시간초과가 발생하는 경우 해시를 적용시켜 해결할 수 있다.

<br/>


## 구현 코드


### Java
- 처음 들어온건 "OK" 출력
- 또 들어온건 "data + 인덱스" 출력


```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Solution {

    static final int HASH_SIZE = 1000;
    static final int HASH_LEN = 400;
    static final int HASH_VAL = 17; // 소수로 할 것

    static int[][] data = new int[HASH_SIZE][HASH_LEN]; // key-data 개수
    static int[] length = new int[HASH_SIZE]; // key의 개수
    static String[][] s_data = new String[HASH_SIZE][HASH_LEN]; // key-문자열 데이터
    static String str;
    static int N;

    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        N = Integer.parseInt(br.readLine()); // 입력 수 (1~100000)

        for (int i = 0; i < N; i++) {

            str = br.readLine();

            int key = getHashKey(str);
            int cnt = checking(key);

            if(cnt != -1) { // 이미 들어왔던 문자열
                sb.append(str).append(cnt).append("\n");
            }
            else sb.append("OK").append("\n");
        }

        System.out.println(sb.toString());
    }

    // key 반환
    // hash function 은 구현마다 달라질 수 있음!!
    public static int getHashKey(String str) {

        int key = 0;

        for (int i = 0; i < str.length(); i++) {
            key = (key * HASH_VAL) + str.charAt(i) + HASH_VAL;
        }

        if(key < 0) key = -key; // 만약 key 값이 음수면 양수로 바꿔주기

        return key % HASH_SIZE;

    }

	// 존재하는 key는 개수 반환
    // 존재하지 않는 key는 -1 반환
    public static int checking(int key) {

        int len = length[key]; // 현재 key에 담긴 수 (같은 key 값으로 들어오는 문자열이 있을 수 있다)

        if(len != 0) { // 이미 들어온 적 있음
            for (int i = 0; i < len; i++) { // 이미 들어온 문자열이 해당 key 배열에 있는지 확인
                if(str.equals(s_data[key][i])) {
                    data[key][i]++;
                    return data[key][i];
                }
            }

        }

        // 들어온 적이 없었으면 해당 key배열에서 문자열을 저장하고 길이 1 늘리기
        s_data[key][length[key]++] = str;

        return -1; // 처음으로 들어가는 경우 -1 리턴
    }

}

```

### 입출력 예시

#### 입력
```
4
apple
banana
abc
abc
```

#### 출력
```
OK
OK
OK
abc1
```

#### 진행 과정

1. apple이 들어옴. key 값을 얻으니 5가 나옴. <br/>
length[5]는 0이므로 처음 들어온 데이터임. <br/>
length[5]++하고 "OK" 출력

2. banana가 들어옴. key 값을 얻으니 3이 나옴. <br/>
length[3]은 0이므로 처음 들어온 데이터임. <br/>
length[3]++하고 "OK" 출력

3. abc가 들어옴. key 값을 얻으니 5가 나옴. <br/>
length[5]는 0이 아님. (즉, 해당 key 값에 누가 들어온적이 있음.) <br/> 
length[5]만큼 반복문을 돌면서 s_data[key]의 배열과 abc가 일치하는 값이 있는지 확인함. <br/>
현재 length[5]는 1이고, s_data[key][0] = "apple"이므로 일치하는 값이 없기 때문에 s_data[key][length[5]]에 abc를 넣고 length[5]를 1 증가시키고 "OK" 출력

4. abc가 들어옴. key 값을 얻으니 5가 나옴. length[5] = 2임. <br/>
s_data[key]를 2만큼 반복문을 돌면서 abc가 있는지 찾음. <br/>
0번 인덱스 값에는 apple이 저장되어 있고 1번 인덱스 값에서 동일한 abc가 있음. (찾았음!) <br/>
따라서 해당 data[key][index] 값을 1 증가시키고 이 값을 return 해주면서 메소드를 끝냄 <br/>
최종적으로 "abc1" 출력 

<br/>

## 관련 문제

- [codeforces : Registration system](https://codeforces.com/contest/4/problem/C)
- [백준 : [1920] 수 찾기](https://www.acmicpc.net/problem/1920)


<br/>

🔖 참고 : [gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/Hash%20Table%20%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.md)
