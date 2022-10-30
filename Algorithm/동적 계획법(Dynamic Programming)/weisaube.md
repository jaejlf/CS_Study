# 동적 계획법(Dynamic Programming)

## 📌 A. 동적 계획법이란?

> 상향식 접근법으로, 가장 작은 문제의 해답을 구한 뒤 이를 저장하여 상위 문제를 풀어가는 방식

<br/>

📚 핵심 단어

- "작은 부분의 해답"
- "저장"
- "상위 문제를 해결"

<br/>

동적 계획의 핵심은 `Memoization(메모이제이션)`

- 동일한 계산을 반복 시, 이전에 계산한 값을 메모리에 저장하여 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 것

<br/>

## 📌 B. 예시 - 재귀 함수와 동적 계획법으로 피보나치 수열 구현

<br/>

### 재귀

<br/>

```Swift
func fibo(_ n: Int) -> Int {
    if n <= 1 { return n }
    return fibo(n - 1) + fibo(n - 2)
}

```

재귀 함수로 `fibo(4)`를 구할 경우 결과를 얻기까지

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb0GAZk%2FbtqT02JFjM0%2FIm3oJdgc9ngJ3QsVFBJ4rk%2Fimg.png" alt="text" width="485" />
</p>

- `fibo(0)`을 구하는 함수를 2번 중복 실행
- `fibo(1)`을 구하는 함수를 3번 중복 실행
- `fibo(2)`를 구하는 함수를 2번 중복 실행해야 함.

👉 하나의 결과를 도출하기까지 중복되는 값을 얻기 위해 실행되는 함수가 너무 많다는 단점이 있음.

<br/>

<br/>

### 동적 계획법

<br/>

```Swift
func fibo(_ n: Int) -> Int{
    var cache: [Int] = [0, 1]

    for num in 2...n {
        cache.append(cache[num - 1] + cache[num - 2])
    }
    return cache[n]
}

```

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBNrUk%2FbtqTKKRWtO2%2FsQXtsMgrhgC43Iyaaqk9M0%2Fimg.png" alt="text" width="485" />
</p>

<br/>

- `cache` 저장 공간을 활용하여 가장 작은 단위인 0, 1부터 도출되는 값을 저장해 나감.
- fibo(4)를 구할 시 4보다 작은 값인 0,1,2,3번째 값까지 먼저 구하여 저장하고, 이 값들이 저장되어 있는 메모리를 이용하여 2번째 index + 3번쨰 Index를 더해 구함.
- 이미 저장되어 있는 값을 활용하기 떄문에 중복 실행을 할 필요가 없음
- 실행 속도 빨라짐

<br/>

## 📌 C. 참고 자료

🔗 [Swift) 동적 계획법 (Dynamic Programming) 이해하기](https://babbab2.tistory.com/100)
