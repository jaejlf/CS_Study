# 💡 힙 정렬 (Heap Sort)

완전 이진 트리(CBT)를 기반으로 하는 힙(Heap) 자료구조를 사용하는 정렬 알고리즘으로, 최소값 혹은 최대값을 먼저 찾고 맨 앞에 배치하는 선택 정렬과 유사하다.

`불안정 정렬(unstable sort)` 에 속한다.

> 🔖 힙(Heap) 설명  
> https://github.com/jaejlf/CS_Study/blob/main/Data%20Structure/%ED%9E%99(Heap)/jihyehann.md

<br/>

## 1. 알고리즘 (오름차순)

1. 정렬해야 할 n개의 요소에 대하여 최대 힙을 구성한다.
2. 루트를 힙의 마지막 원소와 교환한다.
3. 정렬된 마지막 원소를 제외하고 나머지 원소에 대해서 최대 힙으로 재구성하고 2번의 과정을 반복한다.
4. 정렬된 원소를 제외하고 최대 힙에 원소가 1개 남으면 정렬을 종료한다.

![Heap sort](https://user-images.githubusercontent.com/75151848/193419296-07a038ad-bc9c-4997-919e-5cc699e656b5.gif)


<br/>

## 2. 구현 (오름차순)
### Java
```java
public class HeapSort {
  public void sort(int arr[]) {
    int N = arr.length;

    // max heap 초기화
    for (int i = N / 2 - 1; i >= 0; i--)
      heapify(arr, N, i);

    // heap으로부터 원소를 하나씩 추출(extract)
    for (int i = N - 1; i > 0; i--) {
      // 현재 루트를 마지막 노드와 교환
      int temp = arr[0];
      arr[0] = arr[i];
      arr[i] = temp;

      // max heap 재구성
      heapify(arr, i, 0);
    }
  }

  // max heap 구성 메서드
  // N: heap의 size
  // i: index
  void heapify(int arr[], int N, int i) {
    int largest = i; // Initialize largest as root
    int l = 2 * i + 1; // left = 2*i + 1
    int r = 2 * i + 2; // right = 2*i + 2

    // If left child is larger than root
    if (l < N && arr[l] > arr[largest])
      largest = l;

    // If right child is larger than largest so far
    if (r < N && arr[r] > arr[largest])
      largest = r;

    // If largest is not root
    if (largest != i) {
      int swap = arr[i];
      arr[i] = arr[largest];
      arr[largest] = swap;

      // Recursively heapify the affected sub-tree
      heapify(arr, N, largest);
    }
  }
}

```
<br/>

## 3. 시간복잡도

항상 $O(nlogn)$ 의 시간 복잡도를 가진다.

<br/>

## 4. 공간복잡도

추가적인 자료구조를 사용하지는 않으므로 in-place 알고리즘이다.

Auxiliary Space (보조 공간) : $O(1)$

<br/>

## 5. 장점

- 추가적인 배열이 필요하지 않다.(in-palce algorithm, 병합정렬보다 효율적)
- 항상 $O(nlogn)$ 의 시간복잡도를 가진다.
- max 또는 min 값을 구할 때 시간 복잡도는 $O(1)$이다.

<br/>

## 6. 단점

- 일반적으로 속도만 비교하자면 퀵 정렬이 평균적으로 더 빠르다.


<br/>

## 🔖 참고
- [Heap Sort](https://www.geeksforgeeks.org/heap-sort/?ref=lbp)
- [힙 정렬(heap sort)](https://deok2kim.tistory.com/178)
