# 💡 LCA 알고리즘

## 1. LCA (Lowest Common Ancestor) 알고리즘이란?

LCA란, 두 노드의 가장 가까운 공통 조상 노드를 의미하고, LCA 알고리즘은 이러한 최소 공통 조상을 찾는 알고리즘이다.

<img src="https://velog.velcdn.com/images/wisdom-one/post/cb61d6b3-f025-4a4e-9753-a49a0ddbeccb/image.png"
     width="300px"/>

- LCA(2,7) = 1
- LCA(9,6) = 2
- LCA(12,14) = 12

<br/>

## 2. 알고리즘 과정

주어진 두 노드를 u,v라고 하자.

1. 루트 노드의 부모와 depth를 0으로 초기화
2. 모든 노드의 깊이(depth)와 부모 저장
3. LCA 구하기 <br/>
i. u, v 중 더 낮은 곳에 있는 노드를 depth가 같아질 때까지 올린다. <br/>
ii. u, v가 같아질 때까지 두 노드를 모두 올린다.
  
  
<br/>

## 3. 구현 코드

```c++
#include <vector>
#include <queue>
#include <cstdio>
using namespace std;

bool check[50001];
int parent[50001], depth[50001];
vector<int> node[50001];

int lca(int a, int b) {
    if (depth[a] < depth[b])
        swap(a, b);
        
    // 더 낮은 노드를 depth가 같아질 때까지 올린다.
    while (depth[a] != depth[b])
        a = parent[a];
        
    // 두 노드가 같아질 때까지 둘 다 올린다.
    while (a != b) {
        a = parent[a];
        b = parent[b];
    }
    
    // LCA
    return a;
}

int main() {
	int n, m;
    
    // 입력
    scanf("%d", &n);
    for (int i = 0; i < n - 1; i++) {
        int u, v;
        scanf("%d %d", &u, &v);
        node[u].push_back(v);
        node[v].push_back(u);
    }
    
    // 1. 루트 노드 초기화
    depth[1] = 0;
    parent[1] = 0;
    check[1] = true;

    // 2. 모든 노드의 깊이(depth)와 부모 저장
    queue<int> q;
    q.push(1);
    while (!q.empty()) {
        int x = q.front();
        q.pop();
        for (int i = 0; i < node[x].size(); i++) {
            int y = node[x][i];
            if (check[y] == false) {
                depth[y] = depth[x] + 1;
                par[y] = x;
                check[y] = true;
                q.push(y);
            }
        }
    }

    // 3. LCA 구하기
    scanf("%d", &m);
    for (int i = 0; i < m; i++) {
        int a, b;
        scanf("%d %d", &a, &b);
        printf("%d\n", lca(a, b));
    }
}
```
