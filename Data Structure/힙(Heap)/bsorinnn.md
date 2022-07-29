# 힙(Heap)

## A. 들어가기에 앞서

### 1. 우선순위 큐 (Priority Queue)

- 들어온 순서와 상관없이 **우선순위가 높은 데이터**가 항상 먼저 나가는 큐

  - max-priority queue (largest element first)
  - min-priority queue(smallest element first)

- 사용 범위

  이벤트 기반 시뮬레이션(타임스탬프 순서대로 이벤트 수행), Dijkstra 알고리즘, 데이터 압축을 위한 Huffman 부호화 , A\* 알고리즘

- 우선순위 큐의 구현:
  - 배열, 연결리스트, 힙
  - 이중 `힙(heap)`으로 구현하는 것이 가장 효율적

+) 각 구현 방법의 시간 복잡도
|구현 방법|enqueue()|dequeue()|
|---|---|---|
|배열(unsorted array)|O(1)|O(N)|
|연결리스트(unsorted linked list)|O(1)|O(N)|
|정렬된 배열(sorted array)|O(N)|O(1)|
|정렬된 연결 리스트(sorted linked list)|O(N)|O(1)|
|힙(heap)|O(logN)|O(logN)|

<br>

### 2. 트리의 종류

- 이진 트리(Binary Tree): 각 노드가 최대 2개의 자식을 갖는 트리
- 정 이진 트리(Full Binary Tree): 모든 부모 노드가 2개 혹은 0개의 자식을 갖는 트리

    <img src="https://cdn.programiz.com/sites/tutorial2program/files/full-binary-tree_0.png" height=100>

- 포화 이진 트리(Perfect Binary Tree): 모든 internal node가 2개의 자식을 가지고 모든 leaf node들이 같은 레벨에 속하는 트리
  <img src="https://cdn.programiz.com/sites/tutorial2program/files/perfect-binary-tree_0.png" height=100>

- 완전 이진 트리(Complete Binary Tree):

1. 마지막 레벨을 제외하고는 모든 레벨이 완전히 채워져 있다.
2. 마지막 레벨은 꽉 차 있지 않아도 되지만, 노드가 왼쪽에서 오른쪽으로 채워져야 한다.
   <img src="https://cdn.programiz.com/sites/tutorial2program/files/complete-binary-tree_0.png" height=100>

<br>

## B. 힙(Heap)이란?

힙은 최대값 또는 최솟값을 빠르게 찾기 위해 고안된 **완전 이진 트리**

<br>

**힙의 종류**

<img src="https://www.geeksforgeeks.org/wp-content/uploads/MinHeapAndMaxHeap.png" height=100>

<br/>

- 최대힙(max-heap): 부모 노드의 키 값이 자식 노드의 키 값보다 **크거나 같은** 완전 이진 트리
- 최소힙(min-heap): 부모 노드의 키 값이 자식 노드의 키 값보다 **작거나 같은** 완전 이진 트리

- 힙 삽입의 시간 복잡도: `O(log n)`

- 힙 삭제의 시간 복잡도: `O(log n)`

  (\*n은 힙의 노드 개수)

## C. Heap in Swift

일반적으로 `Heap`은 **배열**을 이용해서 구현함.

→ 완전 이진 트리이기 때문에 **노드 간 index 관계**를 나타낼 수 있기 때문

> 완전 이진 트리는 무조건 왼쪽 자식 노드부터 차례로 채워나가기 때문에 노드가 생성되는 순서를 index로 표현 가능!

 <br>

#### 부모 노드와 자식 노드의 관계

```
부모 index = 자식 노드의 index / 2

오른쪽 자식 index = (부모 노드의 index) * 2 + 1

왼쪽 자식 index = (부모 노드의 index) * 2
```

<br>

#### 힙의 삽입

1.힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 삽입

2.새로운 노드를 부모 노드들과 교환

<br>

<p>
<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Heap/Images/Insert1.png" height=100>
<img src="https://github.com/raywenderlich/swift-algorithm-club/blob/master/Heap/Images/Insert2.png?raw=true" height=100>
<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Heap/Images/Insert3.png" height=100>
</p>

#### 힙 구현

```Swift
struct Heap<Element: Equatable> {

  var elements: [Element] = []
  let sort: (Element, Element) -> Bool

  init(sort: @escaping (Element, Element) -> Bool, elements: [Element] = []) {
    self.sort = sort
    self.elements = elements

    if !elements.isEmpty {
      for i in stride(from: elements.count / 2 - 1, through: 0, by: -1) {
        siftDown(from: i)
      }
    }
  }

  func parentIndex(ofChildAt index: Int) -> Int {
    (index - 1) / 2
  }
```

###### 최대 힙 삽입 구현

```Swift
// Copyright (c) 2021 Razeware LLC
// For full license & permission details, see LICENSE.markdown.
  mutating func siftUp(from index: Int) {
    var child = index
    var parent = parentIndex(ofChildAt: child)
    while child > 0 && sort(elements[child], elements[parent]) {
      elements.swapAt(child, parent)
      child = parent
      parent = parentIndex(ofChildAt: child)
    }
  }
```

#### 힙의 삭제

1.최대 힙에서 최대값은 루트 노드이므로 루트 노드가 삭제됨
(최대 힙에서 삭제 연산은 최대값 요소를 삭제하는 것)

2.삭제된 루트 노드에는 힙의 마지막 노드를 가져옴

3.힙을 재구성

<p>
<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Heap/Images/Remove1.png" height=100>
<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Heap/Images/Remove2.png" height=100>
<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Heap/Images/Remove3.png" height=100>
<img src="https://github.com/raywenderlich/swift-algorithm-club/raw/master/Heap/Images/Remove4.png" height=100>
</p>

###### 최대 힙 삭제 구현

```Swift
  mutating func siftDown(from index: Int) {
    var parent = index
    while true {
      let left = leftChildIndex(ofParentAt: parent)
      let right = rightChildIndex(ofParentAt: parent)
      var candidate = parent
      if left < count && sort(elements[left], elements[candidate]) {
        candidate = left
      }
      if right < count && sort(elements[right], elements[candidate]) {
        candidate = right
      }
      if candidate == parent {
        return
      }
      elements.swapAt(parent, candidate)
      parent = candidate
    }
  }
```

## D. 참고자료

🔗 https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html

🔗 https://github.com/raywenderlich/swift-algorithm-club/tree/master/Heap

🔗 https://github.com/raywenderlich/alg-materials/blob/editions/4.0/22-heaps/projects/final/heap-final.playground/Contents.swift

🔗 https://babbab2.tistory.com/109

🔗 https://code-lab1.tistory.com/8
