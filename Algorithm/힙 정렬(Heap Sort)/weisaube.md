# 힙 정렬(Heap Sort)

## A. 힙 정렬이란?

> 트리 기반으로 최대 힙 트리/ 최소 힙 트리를 구성해 정렬하는 방법

<br/>

+) 최대 힙, 최소 힙

- 최대 힙: 내림차순
  - 부모 노드의 키가 자식노드보다 같거나 크다
- 최소 힙: 오름차순
  - 자식 노드의 키가 부모 노드의 키보다 같거나 크다

<br/>

- 최대힙을 구현한 뒤, **루트노드를** **삭제**하여 배열의 맨 마지막에 넣어주고, **깨진 힙을 재구조화**하는 과정을 반복
- **완전 이진 트리**여야 한다.
- 시간복잡도: O(n log n)

<br/>

<img src="https://gmlwjd9405.github.io/images/data-structure-heap/maxheap-insertion.png">

<br/>

### 특징

- 시간 복잡도가 좋은편
- 전체 자료를 정렬하는 것이 아니라 가장 큰 값 몇개만 필요할 때 유용

<br/>

### 시간 복잡도

- Best, Average, Worst 모두 O(nlog₂n)로 동일

<br/>

## B. 참고자료

🔗 https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html
