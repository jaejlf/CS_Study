# 최장 증가 수열(LIS)

## 📌 A. 최장 증가 수열(LIS, Longest Increasing Subsequence)

<br/>

> 어떠한 수열에서 오름차순으로 증가하는 가장 긴 부분수열

<br>

- 이때, 부분 수열의 각 수는 연속될 필요는 없다.

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJtQq4%2FbtqTwXP8poI%2FWo3hu2CPKXwHZi1TmbNM6k%2Fimg.png" alt="text" width="485" />
</p>

<br/>

위의 수열에서 최장 증가 수열을 찾으면 아래와 같다.

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdkyQPQ%2FbtqTrSCbFPo%2FDHpAiu10JTnVWgMYTDl1lk%2Fimg.png" alt="text" width="485" />

**(1,2,3,6,7,9)** 는 전체 수열 중 오름차순으로 증가하는 가장 긴 부분수열이다.

<br/>

## B. 📌 LIS 길이 구하기

<br/>

### 다이나믹 프로그래밍(DP) - `O(N^2)`

<br/>

최장 증가 수열을 찾는 가장 단순한 방법은 완전 탐색이나, 수열에 존재하는 수의 개수가 K개 일 때 1개 이상의 원소를 갖는 모든 부분수열의 가짓수는 2^k 개이므로 매우 비효율적이다.

👉 다이나믹 프로그래밍(DP)로 구현할 수 있다.

<br/>

DP를 사용할 경우

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F03S68%2FbtqTyCrck0y%2F2MgugIB7ZT2Y6wUgYBBVqK%2Fimg.png" alt="text" width="485" />
</p>

#### 구현 방법

어떤 원소에서 끝나는 최장 증가 수열이 있다면, 그 최장 증가 수열의 k를 제외한 모든 다른 원소들은 k보다 작다.

<br/>

따라서 k의 앞 순서에 있는 모든 원소들 중 값이 k보다 작은 원소에 대해, 그 각각의 원소에서 끝나는 최장 증가 수열의 길이를 알고 있다면, k에서 끝나는 최장 증가 수열의 길이도 구할 수 있다.

<br/>

위의 예시에서는 8 이전의 (1,5,4,2,3)의 수열 중 3에서 끝나는 LIS 길이가 (1,2,3)으로 가장 기므로 이들에 현재 수 8을 더한 (1, 2, 3, 8)이 8에서 끝나는 최장 증가 수열이 된다.

<br/>
(출처: Algorithms – Longest Increasing Subsequence in Swift)

```Swift
let list = [1,5,3,1,7,9,3,6,10,2,22]
var cache = Array.init(repeating: 1, count: list.count)


for current in 1..<list.count {
    for old in 0..<current {
      // current 이전의 모든 원소에 대해 그 원소에서 끝나는 LIS 길이 확인
      // 단 이는 현재 수(list[current])가 그 원소(list[old])보다 클 때만 확인
        if list[current] > list[old] {
            cache[current] = max(cache[current], cache[old]+1) // cache[old]+1 : 이전 원소에서 끝나는 LIS에 현재 수를 붙인 새 LIS 길이
        }
    }
}
```

<br>

### 이분 탐색을 이용한 방법 : O(NlogN)`

이분 탐색(Binary Search)을 사용하면 시간 복잡도를 O(NlogN)으로 줄일 수 있다.

이 방법에서는 LIS를 기록하는 배열을 하나 더 두고, 원래 수열에서의 각 원소에 대해 LIS 배열 내에서의 위치를 찾는다.

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fseho100%2Fpost%2Fce83ccec-524d-4a82-a481-650069328237%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-26%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.52.12.png" alt="text" width="485" />
</p>

<br/>

## 📌 C. 참고자료

🔗 [Algorithms – Longest Increasing Subsequence in Swift](https://holyswift.app/algorithms-longest-increasing-subsequence-in-swift/)

🔗 [최장 증가 수열 (LIS, Longest Increasing Subsequence)](https://4legs-study.tistory.com/106)
