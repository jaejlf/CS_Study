## 📍 Tree (트리)

![image](https://user-images.githubusercontent.com/78673570/182016270-6cb28813-5a95-4738-ba16-1c147fb0018d.png)

= '노드'로 이루어진 자료 구조

= 계층 구조(부모 - 자식 관계)

<br>

### 기본 용어

![image](https://user-images.githubusercontent.com/78673570/182016290-c0485977-e31f-48da-bf4c-58810b33fdae.png)


- `노드 (Node)`
    -   트리를 구성하고 있는 기본 요소
    -   노드에는 키 또는 값과 하위 노드에 대한 포인터를 가지고 있음.
    -   A, B, C, D, E, F, G, H, I, J

- `간선 (Edge)`
    -   노드와 노드 간의 연결선

- `루트 노드 (Root Node)`
    -   트리 구조에서 부모가 없는 최상위 노드
    -    root node : A

- `부모 노드 (Parent Node)`
    -   자식 노드를 가진 노드
    -   H, I의 부모 노드는 D

- `자식 노드 (Child node)`
    -   부모 노드의 하위 노드
    -   노드 D의 자식 노드는 H, I

- `형제 노드 (Sibling node)`
    -   같은 부모를 가지는 노드
    -   H, I는 같은 부모를 가지는 형제 노드

- `외부 노드(external node, outer node)`
    -   자식 노드가 없는 노드
    -   \= 단말 노드 (terminal node) = 리프 노드(leaf node)
    -   H, I, J, F, G

- `내부 노드 (internal node, inner node)`
    -   자식 노드 하나 이상 가진 노드
    -   = 비 단말 노드 (non-terminal node) = 가지 노드 (branch node)
    -   A, B, C, D, E

- `깊이 (depth)`
    -   루트에서 어떤 노드까지의 간선(Edge) 수
    -   루트 노드의 깊이 : 0
    -   D의 깊이 : 2

- `높이 (height)`
    -   어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수
    -   리프 노드의 높이 : 0
    -   A 노드의 높이 : 3

<br>

### 특징

-   그래프 일종으로, 사이클이 없는 그래프이다. (= DAG, Directed Acyclic Graphs / 방향성이 있는 비순환 그래프)
-   노드가 N개인 트리는 항상 N-1개의 간선(edge)을 가진다.
-   임의의 두 노드 간의 경로도 유일하다. 즉, 두 개의 정점 사이에 반드시 1개의 경로만을 가진다.
-   한 개의 루트 노드만이 존재하며, 모든 자식 노드는 한 개의 부모 노드만을 가진다.


<br>

### 트리의 종류

`이진 트리 (Binary Tree)`

-   각 노드가 최대 두 개의 자식을 갖는 트리
-   이진 트리 순회
    -   중위(in-order) 순회 : 왼쪽 - 현재 - 오른쪽
    -   전위(pre-order) 순회 : 현재 - 왼쪽 - 오른쪽
    -   후위(post-order) 순회 : 왼쪽 - 오른쪽 - 현재


<br>

`이진 탐색 트리(Binary Search Tree)`

-   '모든 왼쪽 노드와 그 이하의 자식 노드 <= 현재 노드 < 모든 오른쪽 노드와 그 이하의 자식 노드' 라는 조건을 만족하는 이진 트리  
    (모든 값들이 노드를 기준으로 두 가지 방향으로만 탐색하면 되기 때문에, 값을 찾는데 편리하다)

<br>

`완전 이진 트리(Complete Binary Tree)`

-   모든 노드들이 레벨별로 왼쪽부터 순서대로 채워져있는 이진 트리

<br>

`전 이진 트리 (Full Binary Tree)`

-   노드들의 자식이 하나도 없거나, 두개의 자식으로 구성된 경우

<br>

`포화 이진 트리 (Perfect Binary Tree)`

-   전 이진 트리이면서 완전 이진 트리인 경우
-   완전히 채워진 이진 트리
