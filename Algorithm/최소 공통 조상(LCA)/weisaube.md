# 최소 공통 조상

## 📌 A.최소 공통 조상 (LCA, Lowest Common Ancestor)

> 최소 공통 조상은 트리 구조에서 임의의 두 정점이 갖는 가장 가까운 조상 정점을 의미한다.

<br/>

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F78uHr%2FbtqUGS9kDu9%2Fuwq0scujhYEK9ngET1BcqK%2Fimg.png" alt="text" width="485" />
</p>

<br/>

위와 같은 예시 트리 구조에서 13, 15번 정점의 최소 공통 조상은 5번 정점이 된다.

<br/>

## 📌 B. LCA를 선형 탐색으로 구하기: `O(depth)`

<br/>

LCA를 구하는 가장 단순한 방법은 두 포인터를 두고 **가리키는 정점이 같아질 때까지 부모 노드를 거슬로 올라가는** 방법이 있다.

즉 parent[x]를 정점 x의 부모 노드라고 할 때, `x=parent[x]` 연산을 반복하면 된다.

하지만 이 방법은 구하고자 하는 두 정점의 LEVEL(깊이)가 다르면, 동시에 거슬러갈 수 없으므로 올라가기 전 두 정점의 깊이를 동일하게 맞추는 작업이 필요하다.

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1HDLM%2FbtqUGU0sZm8%2FfJ1gVjk9aW0WkuRaxplSZk%2Fimg.png" alt="text" width="485" />
    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fk6tXp%2FbtqUTmtMHmq%2F4VjrmWsrd16De4khMKLjuK%2Fimg.png" alt="text" width="485" />
</p>

두 정점의 깊이가 같으면, 이제 **가리키는 정점이 같아질 때까지** 동시에 거슬러 올라가면 된다.

<br/>

이 방법은 두 정점의 깊이에서부터 최대 root까지의 모든 정점을 선형으로 탐색해야 하므로, 시간 복잡도는 O(depth)가 된다.

<br/>

## C. LCA를 이분 탐색으로 구하기 : `O(log(Depth))`

<br>

이분 탐색을 이용하면 LCA를 더 빠른 log 시간 내 구할 수 있다.

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfRoTo%2FbtqUGS9nFbs%2FpdLsVaM8d36KpmqZojtFf0%2Fimg.png" alt="text" width="485" />
</p>

<br/>

Parent 배열을 2차원으로 두어, Parent[x][k] = "x번 정점의 2^k번째 조상 노드의 번호" 로 둔다.

만약 DFS를 통해 Root부터 트리를 구성한다면, 낮은 깊이의 노드를 반드시 먼저 탐색하므로 다음이 성립한다.

```Swift
Parent[x][k] = Parent[Parent[x][k - 1]][k - 1]
```

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3AjKJ%2FbtqUSqDecdM%2FI76QSxRe1j1dIKWD2fcKNk%2Fimg.png" alt="text" width="485" />
</p>

<br/>

이제 선형 시간에 구하는 방법에서 부모 노드로 거슬러가는 과정을 2의 제곱수만큼 한 번에 건너뛸 수 있다.

만약 13, 4번 정점의 최소 공통 조상을 구한다면, 13번 정점의 깊이를 4번 정점의 깊이로 맞추기 위해

5번 정점으로 바로 거슬러 올라간 뒤, 2번 정점으로 거슬러 올라갈 수 있다.

<br/>

## 📌 C. 참고 자료

🔗 [최소 공통 조상 (LCA, Lowest Common Ancestor)](https://4legs-study.tistory.com/121)
