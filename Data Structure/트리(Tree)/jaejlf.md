# 📍 트리 (Tree)

<img src = "https://user-images.githubusercontent.com/78673570/183255471-be6c9633-3a58-49a4-bc90-b40bcfb7f4cd.png" width="100%">

- `Node`와 `Edge`로 이루어진 비선형 계층적 자료구조
- 계층 구조 (부모 - 자식 관계)
- 그래프의 일종 : `사이클이 없는 연결 그래프(connected and acyclic graph)` or `방향성이 있는 비순환 그래프(DAG, Directed Acyclic Graph)`

<br>

## 특징

- 사이클이 존재하지 않는다. → 그래프와 트리의 차이 !
- 노드가 N개인 트리는 항상 N-1개의 간선(edge)을 가진다.
- 임의의 두 노드 간의 경로는 유일하다. 즉, 두 개의 정점 사이에 반드시 1개의 경로만을 가진다.
- 한 개의 루트 노드만이 존재하며, 모든 자식 노드는 한 개의 부모 노드만을 가진다.

<br>

## 용어

![image](https://user-images.githubusercontent.com/78673570/183255479-8cde9535-956d-4a9b-b266-8d6d265e8c46.png)

<br>

`노드 (Node)`
-   트리를 구성하고 있는 기본 요소
-   노드에는 키 또는 값과 하위 노드에 대한 포인터를 가지고 있음.
-   A, B, C, D, E, F, G, H, I, J

<br>

`간선 (Edge)`
-   노드와 노드 간의 연결선

<br>

`루트 노드 (Root Node)`
-   트리 구조에서 부모가 없는 최상위 노드
-   A
    
<br>

`부모 노드 (Parent Node)`
-   자식 노드를 가진 노드
-   H, I의 부모 노드는 D
   
<br>

`자식 노드 (Child node)`
-   부모 노드의 하위 노드
-   노드 D의 자식 노드는 H, I
    
<br>

`형제 노드 (Sibling node)`
-   같은 부모를 가지는 노드
-   H, I는 같은 부모를 가지는 형제 노드

<br>

`외부 노드(external node, outer node)`

= 단말 노드 (terminal node) = 리프 노드(leaf node)

-   자식 노드가 없는 노드
-   H, I, J, F, G

<br>

`내부 노드 (internal node, inner node)`

= 비 단말 노드 (non-terminal node) = 가지 노드 (branch node)

-   자식 노드 하나 이상 가진 노드
-   A, B, C, D, E

<br>

`깊이 (depth)`
-   루트에서 어떤 노드까지의 간선(Edge) 수
-   루트 노드의 깊이 : 0
-   D의 깊이 : 2

<br>

`높이 (height)`
-   어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수
-   리프 노드의 높이 : 0
-   A 노드의 높이 : 3

<br>

## 트리의 종류

![image](https://user-images.githubusercontent.com/78673570/183255488-eb786e1c-4e88-45a3-8f83-ffbfca571db8.png)

### 이진 트리 (Binary Tree, BT)

- 자식 노드가 최대 2개인 트리

<br>

###  이진 탐색 트리 (Binary Search Tree, BST)

- `모든 왼쪽 노드와 그 이하의 자식 노드 <= 현재 노드 < 모든 오른쪽 노드와 그 이하의 자식 노드` 라는 조건을 만족하는 이진 트리
- 모든 값들이 노드를 기준으로 두 가지 방향으로만 탐색하면 되기 때문에, 값을 찾는데 편리하다.
- 모든 노드는 중복없이 유일한 값을 가진다.

<br>

### 완전 이진 트리 (Complete Binary Tree)

- 모든 노드들이 레벨별로 왼쪽부터 순서대로 채워져있는 이진 트리

<br>

### 전 이진 트리 (Full Binary Tree)

- 노드들의 자식이 하나도 없거나, 두개의 자식으로 구성된 트리

<br>

### 포화 이진 트리 (Perfect Binary Tree)

- 전 이진 트리이면서 완전 이진 트리인 경우
- 완전히 채워진 이진 트리

<br>

## 트리 순회 방식

노드 방문을 언제 하느냐에 따라 3가지 (전위 순회, 중위 순회, 후위 순회)로 나뉘며 추가적으로 레벨 순회 방법도 존재한다.

![image](https://user-images.githubusercontent.com/78673570/183255495-5d803aea-da41-4afa-a973-f63a481cc603.png)

<br>

### 전위 순회 (pre-order)
- node → left → right
- 1 → 2 → 4 → 8 → 9 → 5 → 10 → 11 → 3 → 6 → 13 → 7 → 14

```java
public void preOrder(Node node) {
	if(node != null) {
		System.out.print(node.data + " ");
		if(node.left != null) preOrder(node.left);
		if(node.right != null) preOrder(node.right);
	}
}
```

<br>

### 중위 순회 (in-order)
- left → node → right 
- 8 → 4 → 9 → 2 → 10 → 5 → 11 → 1 → 6 → 13 → 3 →14 → 7

```java
public void inOrder(Node node) {
	if(node != null) {
		if(node.left != null) inOrder(node.left);
		System.out.print(node.data + " ");
		if(node.right != null) inOrder(node.right);
	}
}
```

<br>

### 후위 순회 (post-order)
- left → right → node
- 8 → 9 → 4 → 10 → 11 → 5 → 2 → 13 → 6 → 14 → 7 → 3 → 1

```java
public void postOrder(Node node) {
	if(node != null) {
		if(node.left != null) postOrder(node.left);
		if(node.right != null) postOrder(node.right);
		System.out.print(node.data + " ");
	}
}
```

<br>

### 레벨 순회 (level-order)
- root 노드부터 레벨별로 순회
- 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 13 → 14

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

<br>

🧩 Code. https://github.com/jaejlf/Algorithm/blob/main/Basic_Practice/tree.java
