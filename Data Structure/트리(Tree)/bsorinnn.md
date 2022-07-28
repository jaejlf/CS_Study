# 트리(Tree)

<br>
<img src="https://open4tech.com/wp-content/uploads/2018/12/tree-data-struct.png">
<br>

트리란 노드의 집합으로, 계층을 이루고 있는 데이터 구조를 의미한다.

## 1. 용어 정리

- 트리는 값을 가진 `노드(node)` 와 노드를 연결하는 `간선(edge)`로 이루어져 있다.
- `루트(root)`는 트리 가장 윗부분에 위치한 노드를 말한다. 하나의 트리에는 하나의 루트가 있다.
- `리프(leaf)`는 트리의 가장 아랫부분에 위치한 노드를 뜻한다. `terminal node` 또는 `external node`라고 하기도 한다.
  - `inner node`: 리프를 제외한 노드
- 모든 노드들은 0개 이상의 자식(child) 노드를 가질 수 있다.
- `차수(degree)`는 노드가 갖는 **자식의 수**를 뜻한다. 모든 노드의 차수가 n 이하인 트리를 n진 트리라고 한다.
- `레벨(level)`은 루트로부터 얼마나 떨어져 있는지를 뜻한다. 루트의 레벨은 0, 루트로부터 가지가 하나씩 뻗어나갈 때마다 레벨이 1씩 추가된다.
- `높이(height)` 는 루트로부터 가장 멀리 떨어진 리프까지의 거리를 뜻한다.

<br>
트리의 특징
<br>

<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Tree/Images/Cycles.png">

- 트리에는 사이클이 존재할 수 없다. (사이클이 존재하는 것은 그래프) → 위의 사진은 그래프!
- 노드의 개수가 N개면, 간선은 N-1개를 가진다.

<br>

## 2. 트리 순회 방식

트리를 순회하는 방식은 크게 4가지가 있다. `(5 * (a - 10)) + (-4 * (3 / b))` 표현식을 모델링한 트리로 살펴보도록 하자.

<br>

<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Binary%20Tree/Images/Operations.png">

<br>

1. #### 전위 순회 Pre-Order

   노드 자신 → 노드의 왼쪽 자식 → 노드의 오른쪽 자식

   > '+' → _ → 5 → - → a → 10 → _ → - → 4 → / → 3 → b

2. #### 중위 순회 In-Order(depth-first)

   노드의 왼쪽 자식 → 노드 자신 → 노드의 오른쪽 자식

   > 5 → _ → a → - → 10 → + → 4 → - → _ → 3 → / → b

3. #### 후위 순회 Post-Order
   노드의 왼쪽 자식 → 노드의 오른쪽 자식 → 노드 자신
   > 5 → a → 10 → - → _ → 4 → - → 3 → b → / → _ → +

순회 알고리즘의 시간 복잡도: `O(N)`

(\* n은 노드의 개수)

<br>

## 3. Binary Tree (이진 트리)

<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Binary%20Tree/Images/BinaryTree.png">

이진 트리는 **각각의 노드가 최대 두 개의 자식 노드를 가지는** 트리 자료 구조다.

#### Perfect Binary Tree(포화 이진 트리), Complete Binary Tree(완전 이진 트리), Full Binary Tree(정 이진 트리)

<br>
<img src="https://adrianmejia.com/images/full-complete-perfect-binary-tree.jpg">

- Full Binary Tree(정 이진 트리): 모든 노드가 0개 또는 2개의 자식 노드만 갖는 트리
- Complete Binary Tree(완전 이진 트리): 위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진 트리
- Perfect Binary Tree(포화 이진 트리): 모든 내부 노드가 2개의 자식 노드를 가지고 모든 리프 노드가 동일한 레벨(혹은 깊이)를 가지는 것

<br>

## 4. Tree in Swift

Binary Node in Swift

```Swift
// Copyright (c) 2021 Razeware LLC
// For full license & permission details, see LICENSE.markdown.

public class BinaryNode<Element> {

  public var value: Element
  public var leftChild: BinaryNode?
  public var rightChild: BinaryNode?

  public init(value: Element) {
    self.value = value
  }
}
```

## 5. 참고 자료

📚 보요 시바타, 『Do it! 자료구조와 함께 배우는 알고리즘 입문: C 언어 편』, 이지스퍼블리싱(2017), p,403 ~ 404

🔗 https://github.com/raywenderlich/alg-materials/blob/editions/4.0/

🔗 https://github.com/raywenderlich/swift-algorithm-club/
