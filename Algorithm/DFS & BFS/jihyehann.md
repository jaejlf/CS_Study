# 💡 DFS & BFS

## 그래프 탐색

`그래프` 란, 정점(node)과 그 정점을 연결하는 간선(edge)으로 이루어진 자료구조를 말한다.

그래프 탐색 기법에는 `DFS` 와 `BFS` 가 있으며, **경로를 찾는 문제**에서 활용하게 된다.

그래프에는 사이클이 있을 수 있기 때문에, 그래프 탐색 시에 한 번 방문한 노드는 재방문하지 않도록 처리해야 한다.

<br/>

> #### 📚 트리 순회 vs 그래프 탐색
> `트리` 는 사이클이 없는 연결 그래프다. <br/>
> 
> 트리 순회 기법에는 `전위 순회`, `중위 순회`, `후위 순회`, `레벨 순회`가 있다.

<br/>

## DFS (Depth-First Search, 깊이 우선 순회)

"루트 노드 혹은 임의 노드에서 다음 브랜치로 넘어가기 전에, 해당 브랜치를 모두 탐색하는 방법"

`재귀함수` 나 `스택` 으로 구현한다.

**모든 경로를 방문해야 하는 경우**에 적합하다.

![](https://velog.velcdn.com/images/wisdom-one/post/415eaea1-f927-4685-9259-4a50b6fba6e1/image.gif)


### 시간 복잡도

- 인접 행렬 : $O(V^2)$
- 인접 리스트 : $O(V+E)$

### 구현 코드

```c
#include <vector>
using namespace std;

bool visited[9]; 
vector<int> graph[9];

void dfs(int x) {
	visited[x] = true;
    
    // 인접한 노드 사이즈만큼 탐색 
	for (int i = 0; i < graph[x].size(); i++) { 
		int y = graph[x][i];
		if (!visited[y]) // 방문하지 않은 경우
            dfs(y); // 재귀적으로 방문
	}
}
```

<br/>

## BFS (Breadth-First Search, 너비 우선 탐색)

"루트 노드 또는 임의 노드에서 인접한 노드부터 먼저 탐색하는 방법"

`큐` 를 통해 구현한다.

**최소 비용**을 구할 때 적합하다.

![](https://velog.velcdn.com/images/wisdom-one/post/af9adf45-3ea7-42a6-a6fe-95bb1173a4c5/image.gif)


### 시간 복잡도

- 인접 행렬 : $O(V^2)$
- 인접 리스트 : $O(V+E)$

### 구현 코드

```c
#include <vector>
#include <queue>

using namespace std;

bool visited[9];
vector<int> graph[9];

void bfs(int start) {
    queue<int> q;
    q.push(start); // 첫 노드를 queue에 삽입
    visited[start] = true; // 첫 노드를 방문 처리

    // 큐가 빌 때까지 반복
    while (!q.empty()) {
        int x = q.front();
        q.pop();
        
        // 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for (int i = 0; i < graph[x].size(); i++) {
            int y = graph[x][i];
            if (!visited[y]) {
                q.push(y);
                visited[y] = true;
            }
        }
    }
}
```

<br/>

## 🔖 참고
- [gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/DFS%20%26%20BFS.md)
- [블로그](https://devuna.tistory.com/32)
- [블로그](https://better-tomorrow.tistory.com/entry/DFS-BFS-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
