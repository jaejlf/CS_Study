# 💡 동적 계획법 (Dynamic Programming, DP)


## Dynamic Programming 이란?

큰 문제를 작은 문제로 나눠서 푸는 알고리즘.

이름의 Dynamic은 아무 의미 없고, 이 용어를 처음 사용한 1940년 Richard Bellman이 멋있어보여서 사용했다고 한다.

다음의 2가지 속성을 만족할 경우, Dynamic Programming으로 문제를 해결할 수 있다.

1. Overlapping Subproblem
2. Optimal Substructure

#### Overlapping Subproblem

- 문제를 **겹치는 부분 문제**로 나눌 수 있다. (큰 문제 &rarr; 작은 문제)
- 큰 문제와 작은 문제를 **같은 방법**으로 해결할 수 있다.


#### Optimal Substructure

- 문제의 정답을 작은 문제의 정답에서 구할 수 있다.
- 문제의 크기에 상관없이 작은 문제의 정답은 항상 **일정**하다.

<br/>

## Dynamic Programming의 성질

- 다이나믹 프로그래밍에서 각 문제는 한 번만 풀어야 한다.
- Optimal Substructure을 만족하기 때문에, 같은 문제는 구할 때마다 정답이 같다.
- 정답을 한 번 구했으면 그것을 어딘가에 "메모”해두어야한다.  <br/> 
&rarr; `Memoization` (메모이제이션) <br/> 
&rarr; 배열에 저장

<br/>

## 구현 방식

1. Top-down : 재귀 호출
2. Bottom-up : for문 

<br/> 

### 1. Top-down

1. 문제를 작은 문제로 나눈다. <br/> 
fiboacci(n) &rarr; fibonacci(n-1) + fibonacci(n-2)
2. 작은 문제를 푼다. <br/> 
fibonacci(n-1)과 fibonacci(n-2) 호출
3. 작은 문제를 풀었으니, 이제 문제를 푼다. <br/> 
fibonacci(n-1)과 fibonacci(n-2) 의 값을 더해 문제를 푼다.

```c
int dp[100];
int fibonacci(int n) {
    if (n <= 1) return n;
    else {
      // 이미 구했던 값이라면 메모해 두었던 값을 사용
      if (dp[n] > 0) return dp[n];
      dp[n] = fibonacci(n - 1) + fibonacci(n - 2); 
      return dp[n];
  } 
}
```

<br/> 

### 2. Bottom-up 

1. 문제를 크기가 작은 문제부터 차례대로 푼다. <br/> 
for (int i = 2 ; i <= n ; i++)
2. 문제의 크기를 조금씩 크게 만들면서 문제를 점점 푼다. <br/> 
for (int i = 2 ; i <= n ; i++)
3. 작은 문제를 풀면서 왔기 때문에, 큰 문제는 항상 풀 수 있다. <br/> 
dp[i] = dp[i - 1] + dp[i - 2];
4. 그러다보면, 언젠가 풀어야 하는 문제를 풀 수 있다. <br/> 
dp[n]을 구하게 된다.

```c
int dp[100];
int fibonacci(int n) {
    dp[0] = 1;
    dp[1] = 1;
    for (int i = 2 ; i <= n ; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```
