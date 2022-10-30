# 다익스트라(Dijkstra)

## 📌 A. 다익스트라 알고리즘(Dijkstra Algorithm)

> 다이나믹 프로그래밍을 활용한 대표적인 **최단 경로(Shortest path)** 알고리즘

<br/>

- 하나의 정점에서 다른 모든 정점으로 가는 최단 경로를 알려줌
- 이 때, 음의 간선은 포함할 수 없음(현실 세계에 사용하기 매우 적합한 알고리즘)
- 최단 거리는 여러 개의 최단 거리로 이루어져 있기 때문에, 작은 문제가 큰 문제의 부분 집합에 속해있다 볼 수 있어 DP 문제라 할 수 있음
- 최단 거리를 구할 때 그 이전까지 사용했던 최단 거리 정보를 그대로 사용

<br/>

## 📌 B. 동작 과정

(출처: https://code-lab1.tistory.com/29 [코드 연구소:티스토리])

다익스트라 알고리즘을 구현하기 위해서는 다음과 같은 과정을 반복하면 된다.

1. 방문하지 않은 정점 중 가장 가중치 값이 작은 정점을 방문한다. (처음엔 시작 정점 방문)
2. 해당 정점을 거쳐서 갈 수 있는 정점의 거리가 이전에 기록한 값보다 작다면 그 거리를 갱신한다.

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAto0N%2FbtrbUYDz5FP%2FHP7KdrY1eRvGlOumrckwQK%2Fimg.png" alt="text" width="485" />
</p>
시작정점은 0번 정점이라고 가정하고 나머지 정점까지의 최단거리를 계산해보자.
1차원 배열 dist[]에 각 정점까지의 최단거리를 갱신해 나갈 것이다. 초기에는 모두 INF(무한대)로 설정한다.

<br/>
<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWZExx%2FbtrbLf1a2jH%2FWDKYCg5nR5IV1yhanZDD0K%2Fimg.png" alt="text" width="485" />
</p>
가장 먼저 시작정점을 방문한다.
시작 정점에서 방문 할 수 있는 정점들에 대한 거리를 갱신한다. 

<br/>
<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdmmVC6%2FbtrbU0OS9ni%2FjqNp6o4HSJI6pdTqj2ss9K%2Fimg.png" alt="text" width="485" />
</p>

- 방문하지 않은 정점 중 가장 가중치가 작은 2번 정점을 방문한다
- 0번 정점에서 2번 정점을 거쳐서 4번 정점을 가면 기존 거리 보다 최단 거리이므로 갱신한다 ( INF > 11)
- 0번 정점에서 2번 정점을 거쳐서 3번 정점을 가면 기존 거리 보다 최단 거리이므로 갱신한다 ( 7 > 6 )
  <br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FL3BvB%2FbtrbPcvTgFR%2FFmvnkWkWsHbdvy6mWalJI1%2Fimg.png" alt="text" width="485" />
</p>

- 방문하지 않은 정점 중 가장 가중치가 작은 3번 정점을 방문한다.
- 0번 정점-2번 정점-3번정점을 거쳐서 4번 정점을 가면 기존 거리보다 최단 거리이므로 갱신한다( 11> 10 )

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMQL7X%2FbtrbQ9FngRj%2FHyGqDsuh0Q6hkU0SWDLVgK%2Fimg.png" alt="text" width="485" />
</p>

- 방문하지 않은 정점 중 가장 가중치가 작은 4번 정점을 방문한다.
- 갱신할 거리가 없다.

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbwMaO%2FbtrbVryIsig%2FYwbwLgCoQVevSzZiv8UHoK%2Fimg.png" alt="text" width="485" />
</p>

- 방문하지 않은 정점 중 가장 가중치가 작은 1번 정점을 방문한다.
- 갱신할 거리가 없다.
- 모든 정점을 방문했으므로 종료한다.

위와 같은 과정을 거치면 dist 배열에 0번정점부터 각 정점까지의 최단거리가 기록되게 된다.

<br/>

## 📌 C. 구현 & 시간복잡도

<br/>

```Swift
/**
* Original Code
* https://gist.github.com/stevencurtis/88792de46139f5f80ec23f812e24bb02#file-dijkstrashortestpath
*/

func shortestPath (source: Int, destination: Int, graph: Graph) -> Int {
    var currentNode = graph.nodes.first{ $0.identifier == source }!
    currentNode.visited = true
    currentNode.distance = 0
    var toVisit = [Node]()
    toVisit.append(currentNode)
    while ( !toVisit.isEmpty) {
        toVisit = toVisit.filter{ $0.identifier != currentNode.identifier }
        currentNode.visited = true
        // Go to each adjacent vertex and update the path length
        for connectedEdge in currentNode.edges {
            let dist = currentNode.distance + connectedEdge.weight
            if (dist < connectedEdge.to.distance) {
                connectedEdge.to.distance = dist
                toVisit.append(connectedEdge.to)
                if (connectedEdge.to.visited == true) {
                    connectedEdge.to.visited = false
                }
            }
        }
        currentNode.visited = true
        //set current node to the smallest vertex
        if !toVisit.isEmpty {
            currentNode = toVisit.min(by: { (a, b) -> Bool in
                return a.distance < b.distance
            })!
        }

        if (currentNode.identifier == destination) {
            return currentNode.distance
        }
    }
    return -1
}
```

① 노드마다 인접한 간선을 모두 검사하는 과정 = 𝑂(𝐸)

② 우선순위 큐에 insert/pop 하는 과정 = 𝑂(𝑙𝑜𝑔𝐸)

👉 이 둘을 더한 𝑂(𝐸𝑙𝑜𝑔𝐸)가 다익스트라 알고리즘의 시간복잡도

<br/>

## 📌 D. 참고 자료

🔗 [[알고리즘] 다익스트라(Dijkstra) 알고리즘이란?](https://4legs-study.tistory.com/121)

🔗 [Dijkstra’s Algorithm in Swift](https://medium.com/swift-coding/dijkstras-algorithm-in-swift-488a184fb7a6)
