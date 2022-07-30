# 💡 Tree

- Node와 Edge로 이루어진 비선형 계층적 자료구조.
- 그래프의 일종으로, **사이클이 없는 연결 그래프**(connected and acyclic graph)를 말한다.

<img src="https://user-images.githubusercontent.com/75151848/181903174-64f4a29d-894b-463d-8f8f-885b9bc0aa16.png" height="260"/>

<br/><br/>

## ✔️ 용어

![term](https://user-images.githubusercontent.com/75151848/181903525-a18ada9c-089e-4cd6-954b-f49a43f494a5.png)

<br/>

| 용어 | 설명 |
| --- | --- |
| Node | 데이터와 링크 필드로 구성된 트리의 단위 |
| Edge (간선) | 노드와 노드 사이의 연결선 |
| Root node | 부모 노드가 없는 최상위 노드 |
| Parent node (부모 노드) | 자식 노드를 가진 노드 |
| Child node (자식 노드) | 부모 노드의 하위 노드 |
| Sibling node (형제 노드) | 같은 부모를 가지는 노드 |
| External node (외부 노드) <br/> Terminal node (단말 노드) <br/> Leaf node (리프 노드) | 자식 노드가 없는 노드 |
| Internal node, Inner node (내부 노드) <br/> Non-terminal node (비 단말 노드 ) <br/> Branch node (가지 노드) | 하나 이상의 자식 노드를 가진 노드 |
| Depth (깊이) | 루트에서 어떤 노드까지의 간선(Edge) 수 |
| Height (높이) | 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수 |
| Level | 루트에서 어떤 노드까지의 간선(Edge) 수 |
| Degree (차수) | 노드의 자식 수 <br/> Leaf node의 degree는 항상 0 이다. |
| Path (경로) | 한 노드에서 다른 한 노드에 이르는 길 사이에 놓여있는 노드들의 순서 |

<br/><br/>

## ✔️ 특징

- **사이클**이 존재하지 않는다. → **그래프와 트리의 차이❗️**
- 루트에서 한 노드로 가는 경로는 유일하다.
- 루트노드를 제외한 모든 노드는 단 하나의 부모 노드를 가진다.
- 노드의 개수가 N개면, 간선은 N-1개를 가진다.

<br/><br/>

## ✔️ 트리 순회 (Tree **traversal)**

노드 방문을 언제 하느냐에 따라 일반적으로 3가지 순회 방법으로 나누며, 추가적으로 레벨 순회 방법도 존재한다.

<br/>

### 전위 순회 (Preorder)

- **node** → left child → right child 순으로 방문

```java
public void preOrder(Node node) {
	if(node != null) {
		System.out.print(node.data + " ");
		if(node.left != null) preOrder(node.left);
		if(node.right != null) preOrder(node.right);
	}
}
```

<br/>


### 중위 순회 (Inorder)

- left child → **node** → right child 순으로 방문

```java
public void inOrder(Node node) {
	if(node != null) {
		if(node.left != null) inOrder(node.left);
		System.out.print(node.data + " ");
		if(node.right != null) inOrder(node.right);
	}
}
```

<br/>


### 후위 순회 (Postorder)

- left child → right child → **node** 순으로 방문

```java
public void postOrder(Node node) {
	if(node != null) {
		if(node.left != null) postOrder(node.left);
		if(node.right != null) postOrder(node.right);
		System.out.print(node.data + " ");
	}
}
```

<br/>


### 레벨 순회 (Level-order)

- 루트에서부터 같은 레벨에 있는 모든 노드를 왼쪽에서 오른쪽 방향으로 방문한 뒤, 하위 레벨로 내려가서 이 과정을 반복한다.
- `Queue` 를 이용하여 구현할 수 있다.

```java
public void levelOrder(Node root) {
	Queue<Node> queue = new LinkedList<>();
	queue.offer(root);

	while(!queue.isEmpty()) {
		Node node = queue.poll();
		System.out.print(node.data + " ");

		if(node.left != null) queue.offer(node.left); // 왼쪽 자식 노드가 있다면 추가 
		if(node.right != null) queue.offer(node.right); // 오른쪽 자식 노드가 있다면 추가 
	}
}
```

<br/><br/>

## ✔️ 트리 종류


### 이진 트리(**Binary Tree,** BT)

- 2개 이하의 자식노드를 가지는 트리.

<br/>

### 이진 탐색 트리(**Binary Search Tree,** BST)

- 이진 트리의 한 종류
- 모든 노드는 중복 없이 유일한 값을 가진다.
- left node에는 부모 노드보다 작은 값이 저장되고, <br/> 
right node에는 부모 노드보다 큰 값이 저장된다.
- **시간 복잡도** <br/><br/>
  |  | Average Case | Worst Case |
  | --- | --- | --- |
  | 검색 | O(logN) | O(N) |
  | 삽입 | O(logN) | O(N) |
  | 삭제 | O(logN) | O(N) |
  | 순회 | O(N) | O(N) |

<br/>

### 최소 신장 트리 (Minimum Spanning Tree, MST)

- **`Spanning Tree`** (신장 트리)
    - 그래프의 최소 연결 부분 그래프.
    - n개의 정점을 가지는 그래프에서 (n-1)개의 간선으로 연결되어 있는 그래프. 
    이 조건을 만족하면, 해당 부분 그래프는 필연적으로 트리의 형태가 된다.
    
    ❗️ **ST를 찾기 위한 방법은?** `DFS` 혹은 `BFS` 를 통해 그래프 탐색을 하여 구한다.
    
- **`Minimum Spanning Tree`** (최소 신장 트리)
    - Spanning Tree 중에서 사용된 간선들의 가중치 합이 최소인 트리.
    
    ❗️ **MST를 찾기 위한 방법은?** `Kruskal의 알고리즘` 혹은 `Prim의 알고리즘` 을 통해 구한다.
    
<br/><br/><br/>


##  📌 참고

- [https://yoongrammer.tistory.com/68](https://yoongrammer.tistory.com/68)
- [https://velog.io/@kimdukbae/자료구조-트리-Tree](https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%A6%AC-Tree)
- [https://minhamina.tistory.com/83](https://minhamina.tistory.com/83)
- [https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html](https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html)

<br/><br/>
