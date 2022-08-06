# 📍 힙 (Heap)

- 완전 이진트리의 일종으로 `우선순위 큐`를 위해 만들어진 자료구조
- 여러 값들 중 '최댓값' 혹은 '최솟값'을 빠르게 찾아내도록 만들어진 자료구조
- 트리 구조이기 때문에 삽입/삭제는 `O(nlogn)`으로 매우 빠르다.

<br>

## 종류

![image](https://user-images.githubusercontent.com/78673570/183255659-5b8c08a3-99ea-4aaf-a423-8a3e435c9db5.png)

- `최대 힙 (Max Heap)` : 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
- `최소 힙 (Min Heap)` : 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리

<br>

## Heap에 요소 삽입 & 삭제

### index

루트 노드는 1, 형제 노드끼리는 왼쪽 - 오른쪽순으로 인덱스를 부여한다.

```sql
- 왼쪽 자식 노드의 index = 부모 노드의 index * 2
- 오른쪽 자식 노드의 index = 부모 노드의 index * 2 + 1
- 부모 노드의 index = 자식 노드의 index / 2
```

<br>

### 삽입

(Max Heap 삽입 예제)

<img src="https://user-images.githubusercontent.com/78673570/183255664-83009fd7-8797-4471-9629-bcbf4e8f3975.png" width="70%">

1. 힙에 새로운 요소가 들어오면, 가장 마지막 위치에 삽입한다.
2. 부모 노드와 비교하면서, 최대힙/최소힙의 성질에 맞게 재구성한다.

<br>

### 삭제

(Max Heap 삭제 예제)

<img src="https://user-images.githubusercontent.com/78673570/183255670-4875bf33-b939-4269-bd2e-e701b8684ae5.png" width="70%">

1. 루트 노드를 삭제한다.
2. 삭제된 루트 노드의 자리에 힙의 마지막 노드를 가져온다.
3. 부모 노드와 비교하면서, 최대힙/최소힙의 성질에 맞게 재구성한다.

<br>

### 구현

🧩 Max Heap Code. https://github.com/jaejlf/Algorithm/blob/main/Basic_Practice/max_heap.java

🧩 Min Heap Code. https://github.com/jaejlf/Algorithm/blob/main/Basic_Practice/min_heap.java
