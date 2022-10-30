# 📍 동적 계획법(Dynamic Programming)

- 프로그램이 실행되는 도중에 실행에 필요한 메모리를 할당하는 기법
- 이미 계산된 결과(하위 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 설계함으로써 메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 방법
- 
<br>

## DP 문제가 성립할 조건

1. 최적 부분 구조(Optimal Substructure) : 상위 문제를 하위 문제로 나눌 수 있으며 하위 문제의 답을 모아서 상위 문제를 해결할 수 있다.
2. 중복되는 부분 문제(Overlapping Subproblem) : 동일한 작은 문제를 반복적으로 해결해야 한다.

=> 대표적인 것이 '피보나치 수열'

<br>

## 구현 방법

예시) 피보나치 수열
![image](https://user-images.githubusercontent.com/78673570/198875238-1cf4ee79-acaa-4f61-b33e-25beb57a9995.png)

<br>

### Top-down 하향식
- 상위 문제를 해결하기 위해서 하위 문제를 재귀적으로 호출하여 하위 문제를 해결함으로써 상위 문제를 해결하는 방식
- 하위 문제를 저장해 놓기 위해 Memoization 사용
```java
public class Topdown {
	static int[] dp;
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		dp  = new int[n + 1];
		System.out.println(fibo(n));
		
	}
  
	static int fibo(int x) {
		if(x == 1 || x == 2) return 1;
		if(dp[x] != 0) return dp[x];
		dp[x] = fibo(x-1) + fibo(x-2);
		return dp[x];
	}
}
```

<br>

### Bottom-up 상향식
- 하위에서부터 문제를 해결해나가면서 먼저 계산했던 문제들의 값을 활용해서 상위 문제를 해결해나가는 방식
- DP의 전형적인 구현 방식으로, 반목문을 사용해서 구현
```java
public class Bottomup {

	static int[] dp;
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		dp  = new int[n + 1];
		System.out.println(fibo(n));
	}
	
	static int fibo(int x) {
		dp[1] = 1;
		dp[2] = 1;
		for(int i = 3; i < x + 1; i++) {
			dp[i] = dp[i - 1] + dp[i - 2];
		}
		return dp[x];
	}
}
```

<br>

🥨 메모이제이션(Memoization)
- 한 번 계산한 결과를 메모리 공간에 메모하는 기법
- 모든 부분 문제가 한 번씩만 계산된다고 보장할 수 있기 때문에 함수 호출 횟수를 엄청나게 감소시킬 수 있다.
- 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져온다.
- 값을 기록해 놓는다는 점에서 캐싱(Cachig)이라고 한다.
