# DFS & BFS

## 📌 A. DFS와 BFS의 차이

DFS와 BFS 모두 그래프를 탐색하는 방법이다.

- 그래프는 정점(node)와 정점을 연결하는 간선(edge)로 이루어진 자료구조의 일종이다.
- 그래프를 탐색한다는 것은 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것을 말한다.

<br/>

### **DFS**

> 깊이 우선 탐색 (Depth-First Search)

<br/>

- 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방식
- 최대한 **멀리 있는** 노드 우선 탐색
- **스택** 자료구조 또는 **재귀함수** 이용
  - → 선입후출

<br/>

### **BFS**

> 너비 우선 탐색 (Breadth-First Search)

<br/>

- 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법
- 위에서 아래로, 왼쪽에서 오른쪽 순으로 **가까운 노드**부터 탐색
- 모든 간선의 길이(비용)이 동일할 때 이용
- 주로 **두 노드 사이의 최단 경로**를 찾고 싶을 때 이 방법을 선택
- **큐** 자료구조 이용
  - → 선입선출

<br/>

<p align="center">
  <img src="https://iq.opengenus.org/content/images/2020/05/dfs-vs-bfs.gif" alt="text" width="485" />
</p>

<br/>

## 📌 B. DFS

> 탐색하려는 노드의 자식 노드부터 우선 탐색하는 방식

<br/>

탐색 노드의 인접 자식 노드들을 모두 탐색하고 난 후에 다시 돌아가서 탐색 노드의 다른 인접 자식 노드들을 모두 탐색하는 방법<br/>

(이때 왼쪽을 먼저 탐색할지, 오른쪽을 먼저 탐색할지와 같은 순서는 중요하지 않음)

<br/>

👉 해당 노드의 가장 깊은 노드까지 우선 탐색해야 다음 노드를 탐색할 수 있음.

<br/>

```Swift
func dfs(_ start: Int) {
    visit[start] = true // 1.방문
    print(start, terminator: " ")

    // 2. 방문할 리스트
    for end in 1...N {
        if map[start][end] == 1, !visit[end] {
            visit[end] = true
            dfs(end) // 3. 정해진곳 방문 후 1번으로 다시
        }
    }
}
```

<br/>

② DFS를 재귀로 구현한 방법

```Swift
// sourced from https://github.com/raywenderlich/swift-algorithm-club/tree/master/Depth-First%20Search


func depthFirstSearch(_ graph: Graph, source: Node) -> [String] {
  var nodesExplored = [source.label]
  source.visited = true

  for edge in source.neighbors {
    if !edge.neighbor.visited {
      nodesExplored += depthFirstSearch(graph, source: edge.neighbor)
    }
  }
  return nodesExplored
}
```

- DFS의 시간복잡도: `O(V+E)`

<br/>

## 📌 C. BFS

> 인접한 노드들을 우선 탐색하는 방법

같은 레벨에 있는 노드들부터 탐색하는 것. (역시 오른쪽, 왼쪽 순서는 중요하지 않음)

👉 같은 레벨에 있는 노드를 먼저 다 탐색해야 다음 레벨 노드를 탐색할 수 있다.

<br/>

```Swift
func bfs() {
  var q = [Int]()
  var ans = ""
	var idx = 0
  q.append(s)
  var visited = [Bool](repeating: false, count: n+1)
  visited[s] = true

  while idx < q.count {
    idx += 1
    ans = ans + "\(next) "

    for val in arr[next] where !visited[val] {
      q.append(val)
      visited[val] = true
    }
  }

  print(ans)
}
```

1. 방문
2. 근처 노드들을 Queue에 삽입
3. Queue에서 하나 빼낸 후 다시 1번부터 시작

<br/>

- BFS의 시간복잡도 : `O(V+E)`

<br/>

## 📌 C. 참고 자료

🔗 [[swift - algorithm] 순열과 조합 (dfs로 구현), bfs, dfs, 백트래킹, 재귀](https://ios-development.tistory.com/423)

🔗 [Swift) 깊이 우선 탐색(DFS) 구현 해보기](https://babbab2.tistory.com/107)

🔗 [Swift) 너비 우선 탐색(BFS) 구현 해보기](https://babbab2.tistory.com/106)

🔗 [raywenderlich - swift algorithm club: Depth -First Search](https://github.com/raywenderlich/swift-algorithm-club/tree/master/Depth-First%20Search)
