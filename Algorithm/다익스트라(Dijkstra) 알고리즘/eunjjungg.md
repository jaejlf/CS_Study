![image](https://user-images.githubusercontent.com/100047095/198876678-6e9658a3-7404-4bb8-b305-141bb261bdba.png)

# 1. 다익스트라 알고리즘

- 그래프에서 한 노드에서 다른 노드까지의 최단 경로를 구하는 알고리즘
- 도착 정점 뿐 아니라 다른 모든 정점까지 최단 경로로 방문하여 각 정점까지의 최단 경로를 한 번에 찾게 됨.

<br/>

**동작 단계**

1. 출발 노드와 도착 노드 설정
2. 최단 거리 테이블 초기화
3. 현재 노드와 인접한 노드 중 방문하지 않은 노드를 구별하고 방문하지 않은 노드 중 가장 짧은 노드를 선택함. 그 노드를 방문 처리함. 
4. 해당 노드를 거쳐 다른 노드로 넘어가는 edge 비용(가중치)을 계산하여 최단 거리 테이블을 업데이트함
5. 3~4번 과정을 반복

<br/>

**특징**

1. 가중치가 양수일 때만 사용할 수 있음
2. 구현 방식은 방문하지 않은 노드를 다루는 방식에서 순차 탐색을 할 것인지 우선순위 큐를 사용할 것인지에 따라 나뉨
3. 시간 복잡도
    1. 인접 행렬로 구현 시 시간 복잡도는 O(n^2)
    2. 인접 리스트로 구현 시 시간 복잡도는 O(nlogn)

<br/>

**구현 코드**

```jsx
import java.io.BufferedReader
import java.io.BufferedWriter
import java.io.InputStreamReader
import java.io.OutputStreamWriter

import java.util.*
import java.util.function.BiFunction
import kotlin.collections.ArrayList
import kotlin.collections.HashMap
import kotlin.math.max
import kotlin.math.min
import kotlin.text.StringBuilder

var br = BufferedReader(InputStreamReader(System.`in`))
var bw = BufferedWriter(OutputStreamWriter(System.out))

val INF = 3000001

var V = 0
var E = 0
var K = 0
var graph = ArrayList<ArrayList<Edge>>()
lateinit var dist : Array<Int>

fun solution() {

    var strtok = StringTokenizer(br.readLine())
    V = strtok.nextToken().toInt()
    E = strtok.nextToken().toInt()

    K = br.readLine().toInt()

    for(i in 0.. V)
        graph.add(ArrayList())

    for(i in 0 until E)
    {
        strtok = StringTokenizer(br.readLine())
        var from = strtok.nextToken().toInt()
        var to = strtok.nextToken().toInt()
        var weight = strtok.nextToken().toInt()

        graph.get(from).add(Edge(from, to, weight))
    }

    dist = Array(V + 1, {INF})
    dist[K] = 0

    dijkstra()

    dist.filterIndexed { index, i -> index > 0 }.forEach {
        if(it == INF)
            bw.write("INF")
        else
            bw.write(it.toString())
        bw.newLine()
    }
}

fun dijkstra()
{
    var visited = BooleanArray(V + 1)

    var queue = PriorityQueue<Node>(kotlin.Comparator { o1, o2 -> o1.distance - o2.distance })
    queue.offer(Node(K, dist[K]))

    while(!queue.isEmpty())
    {
        var now = queue.poll()

        if(visited[now.num])
            continue
        visited[now.num] = true

        for(i in 0 until graph[now.num].size)
        {
            var next = graph[now.num][i]

            if(dist[next.to] > dist[now.num] + next.weight)
            {
                dist[next.to] = dist[now.num] + next.weight

                if(!visited[next.to])
                    queue.offer(Node(next.to, dist[next.to]))
            }
        }
    }
}

data class Edge(var from : Int, var to : Int, var weight : Int)
data class Node(var num : Int, var distance : Int)

fun main() {
    solution()

    br.close()
    bw.close()
}
```

출처 : [https://skytitan.tistory.com/197](https://skytitan.tistory.com/197)
