# 📍 DFS (Depth First Search)

![dfs](https://user-images.githubusercontent.com/78673570/197378789-03b4e0eb-cc5d-4bcc-b3e3-156d85e9c4e3.gif)

- 깊이 우선 탐색
- 모든 노드를 방문하고자 하는 경우에 이 방법을 선택한다.
- 깊이 우선 탐색(DFS)이 너비 우선 탐색(BFS)보다 좀 더 간단하다.
- 검색 속도 자체는 너비 우선 탐색(BFS)에 비해서 느리다.
- 스택 또는 재귀함수로 구현

<br>

## 구현

```java
void dfs(int x) {
	visited[x] = true;  // 방문 처리
    for (int i = 1; i <= V; i++) {
    	if (graph[x][i] == 1 && !visited[i]) {  // 방문하지 않았고 인접노드 일 경우
        	dfs(i);
        }
    }
}
```

<br><br>

# 📍 BFS (Breadth First Search)

![bfs](https://user-images.githubusercontent.com/78673570/197378839-caf9588a-ff31-46ff-a472-a9f80d45f818.gif)
 
- 너비 우선 탐색
- 주로 두 노드 사이의 최단 경로를 찾고 싶을 때 이 방법을 선택한다.
- 큐를 이용해서 구현

<br>

## 구현

```java
void BFS(int v, int start) {
	Queue<Integer> q = new LinkedList<>();  // 큐 초기화
    boolean[] visited = new boolean[v+1];  // 방문한 노드 체크하는 배열
    visited[start] = true;
    q.add(start);
    
    while (!q.isEmpty()) {
    	int now = q.poll();
        for (int i = 1; i <= v; i++) {
        	if (graph[now][i] == 1 && !visited[i]) { // 방문하지 않은 인접 노드
            	visited[i] = true;
                q.add(i);
            }
        }
    }
}
```

<br><br>

# 📍 DFS vs BFS 시간 복잡도 비교

두 방식 모두 조건 내의 모든 노드를 검색한다는 점에서 시간 복잡도는 동일하지만, 일반적으로 DFS를 재귀함수로 구현한다는 점에서 DFS보다 BFS가 더 빠르게 동작한다고 할 수 있다.
