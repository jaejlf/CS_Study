# 📍 최소 공통 조상(LCA, Lowest Common Ancestor)

![image](https://user-images.githubusercontent.com/78673570/198874494-0a1f8c7c-b537-4474-ae08-677f511a2fd2.png)

- 트리 상의 정점 U와 V가 주어질 때 U 와 V에서 가장 가까운 공통 조상
- 최소 공통 조상 알고리즘 = 두 노드에서 가장 가까운 공통 조상을 찾는 알고리즘

<br>

## 동작 과정

![image](https://user-images.githubusercontent.com/78673570/198874615-5b8eaa94-b811-4a74-bb0e-d5473875eecc.png)

0 . U 노드와 V 노드를 정한다. (깊이가 더 큰 노드를 V로 정한다.)

1 . U 노드의 깊이와 V 노드의 깊이가 같아질 때까지 깊이가 더 깊은 노드(V)를 자신의 조상으로 바꾸어 준다.

2 . U 노드와 V 노드의 조상이 같아질 때까지 자신의 조상으로 바꾸어 준다.

<br>

## 구현
```java
public static class LCA {
    private int nodeCount;
    private List<Integer>[] adjacencyList;
    private int treeHigh;
    private int[] depth;
    private boolean[] memoization;
    private int[][] parent;

    public LCA(int nodeCount, List<Integer>[] adjacencyList) {
        this.nodeCount = nodeCount;
        this.adjacencyList = adjacencyList;
        this.memoization = new boolean[nodeCount + 1];
        this.depth = new int[nodeCount + 1];
        getTreeHigh();
        this.parent = new int[nodeCount + 1][this.treeHigh];
    }
  
    // 1 . 그래프의 깊이를 구한다.
    private void getTreeHigh() {
        this.treeHigh = (int) Math.ceil(Math.log(nodeCount) / Math.log(2)) + 1;
    }
    
    // 2 . DFS 로 순회하면서 depth 배열과 parent[][0] 배열을 초기화
    private void init(int current, int treeHigh) {
        memoization[current] = true;
        depth[current] = treeHigh;
        for (int next : adjacencyList[current]) {
            // 메모이제이션
            if (memoization[next])
                continue;
            init(next, treeHigh + 1);
            parent[next][0] = current;
        }
    }
  
    // 3 . parent[x][y] 배열을 세팅
    private void makeParentArray() {
        for (int i = 1; i < treeHigh; i++) {
            for (int j = 1; j < nodeCount + 1; j++) {
                parent[j][i] = parent[parent[j][i - 1]][i - 1];
            }
        }
    }

    public int run(int a, int b) {
        init(1, 1);
        makeParentArray();
        // b 가 더 깊도록 a <-> b
        if (depth[a] > depth[b]) {
            int temp = a;
            a = b;
            b = temp;
        }
        // 깊이가 동일하도록 b를 옮김
        for (int i = treeHigh - 1; i >= 0; i--) {
            if ((1 << i) <= depth[b] - depth[a]) {
                b = parent[b][i];
            }
        }

        if (a == b)
            return a;

        for (int i = treeHigh - 1; i >= 0; i--) {
            if (parent[a][i] != parent[b][i]) {
                a = parent[a][i];
                b = parent[b][i];
            }
        }
        return parent[a][0];
    }
}
```
