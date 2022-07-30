# 💡 Heap

- [우선순위 큐](https://github.com/jaejlf/CS-Study/blob/main/Data%20Structure/%EC%8A%A4%ED%83%9D(Stack)%20%26%20%ED%81%90(Queue)/jihyehann.md#3-priority-queue)를 위하여 만들어진 자료구조.
- **`완전 이진 트리`** (Complete Binary Tree, CBT)의 일종이다.
    - 루트부터 단말 노드 방향으로, 왼쪽에서 오른쪽 방향으로 빈 노드가 없이 순서대로 모든 노드가 존재하는 이진 트리.
    - **`포화 이진 트리`** (Full Binary Tree, FBT)의 단말 노드를 오른쪽에서부터 제거하여 얻어진 트리라고 할 수 있으며, 포화 이진 트리 역시 완전 이진 트리이다.

![image](https://user-images.githubusercontent.com/75151848/181934341-eaf20ac9-030f-445b-b939-f3f3af5bc6bf.png)

<br/><br/>

## ✔️ 종류

### 최대 힙 (Max Heap)

- 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리

### 최소 힙 (Min Heap)

- 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리

<br/>

<img src="https://user-images.githubusercontent.com/75151848/181934211-ecd2703e-4fbd-477f-b18e-e7c9774a1d3d.png" width="80%"/>

<br/><br/>

## ✔️ 구현 (배열)
### 성질
```
* 왼쪽 자식 index = (부모 index) * 2

* 오른쪽 자식 index = (부모 index) * 2 + 1

* 부모 index = (자식 index) / 2
```

<br/>


### 삽입: O(logN)

1. 새로운 노드를 마지막 노드에 삽입한다.
2. min heap 혹은 max heap 조건을 만족하는 동안, 새로운 노드를 부모 노드들과 교환한다.

<br/>

min heap과 max heap은 while문 조건식만 다르다.

#### 📌 Min Heap 삽입

```java
public void insert(int val) {
    // 1. 새로운 노드를 마지막 노드에 삽입
    heap.add(val);

    int p = heap.size()-1;    // p는 새로 삽입한 노드의 인덱스
		
    // 2. 부모가 자식보다 클 동안, 새로운 노드를 부모 노드와 교환 (min heap)
    while(p > 1 && heap.get(p/2) > heap.get(p)) {
        int tmp = heap.get(p/2);  //부모 노드의 값
        heap.set(p/2, val);
        heap.set(p, tmp);

        p /= 2; // 부모 노드로 이동
    }
}
```

#### 📌 Max Heap 삽입

```java
public void insert(int val) {
  // 1. 새로운 노드를 마지막 노드에 삽입
    heap.add(val);

    int p = heap.size()-1;  // p는 새로 삽입한 노드의 인덱스
		
    // 2. 부모가 자식보다 작을 동안, 새로운 노드를 부모 노드와 교환 (max heap)
    while(p > 1 && heap.get(p) > heap.get(p/2)) {
        int tmp = heap.get(p/2);  //부모 노드의 값
        heap.set(p/2, val);
        heap.set(p, tmp);

        p /= 2; // 부모 노드로 이동
    }
}
```

<br/>

### 삭제: O(logN)

1. 루트 노드를 삭제한다.
2. 루트 노드에 마지막 노드를 넣는다.
3. 힙을 재구성한다.

<br/>

min heap과 max heap은 부모와 교환할 자식 노드를 결정하는 조건문의 식과 종료 조건식만 다르다.

#### 📌 Min Heap 삭제

```java
public int delete() {
    // 힙이 비어있으면 0 리턴
    if(heap.size() -1 < 1) {
        return 0;
    }

    // 1. 루트 노드 삭제
    int deleteitem = heap.get(1);

    // 2. 루트 노드에 마지막 노드 삽입
    heap.set(1,heap.get(heap.size()-1));
    heap.remove(heap.size()-1);

    int pos = 1; // 루트에 새로 삽입한 노드의 인덱스

    // 3. 힙 재구성
    while((pos*2) < heap.size()) {

        // 왼쪽 자식과 오른쪽 자식 중 더 작은 값을 min에 넣는다.
        int min = heap.get(pos*2); 
        int minPos = pos*2;
        if(((pos*2+1) < heap.size()) && min > heap.get(pos*2+1)) {    
            min = heap.get(pos*2+1);
            minPos = pos*2+1;
        }

        // 부모가 더 작으면 종료
        if(min > heap.get(pos))
            break;

        // 부모 자식 swap
        int tmp = heap.get(pos);
        heap.set(pos,heap.get(minPos));
        heap.set(minPos, tmp);
        pos = minPos;
    }

    return deleteitem;
}
```

#### 📌 Max Heap 삭제

```java
public int delete() {
    // 힙이 비어있으면 0 리턴
    if(heap.size()-1 < 1) {
        return 0;
    }

    // 1. 루트 노드 삭제
    int deleteitem = heap.get(1);

    // 2. 루트 노드에 마지막 노드 삽입
    heap.set(1,heap.get(heap.size()-1));
    heap.remove(heap.size()-1);

    int pos = 1;  // 루트에 새로 넣은 노드의 인덱스

    // 3. 힙 재구성
    while((pos*2) < heap.size()) {

        // 왼쪽 자식과 오른쪽 자식 중 더 큰 값을 max에 넣는다.
        int max = heap.get(pos*2);
        int maxPos = pos*2;
        if((pos*2 + 1) < heap.size() && max < heap.get(pos*2+1)) {
            max = heap.get(pos*2+1);
            maxPos = pos*2+1;
        }

        // 부모가 더 크면 종료
        if(heap.get(pos) > max){
            break;
        }

        // 부모 자식 swap
        int tmp = heap.get(pos);
        heap.set(pos, max);
        heap.set(maxPos, tmp);
        pos = maxPos;
    }
    return deleteitem;
}
```

<br/><br/>

## 📌 참고

- [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)
- [https://st-lab.tistory.com/205](https://st-lab.tistory.com/205)

<br/><br/>
