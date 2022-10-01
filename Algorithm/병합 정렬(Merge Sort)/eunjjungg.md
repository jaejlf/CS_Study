# 1. 병합 정렬

> 큰 문제를 작은 2개의 문제로 나눈 다음 해결한 후 결과를 모아 원래의 큰 문제를 해결하는 Divide and Conquer, 분할 정복 알고리즘의 하나임.<br/>
리스트를 작은 크기로 나눈 다음 규칙에 맞춰 합쳐가며 정렬을 하는 알고리즘임.
> 

![image](https://user-images.githubusercontent.com/100047095/193398385-c569b315-ae6d-4f68-b0b9-29f594f36746.png)

출처 : [https://levelup.gitconnected.com/visualizing-designing-and-analyzing-the-merge-sort-algorithm-cf17e3f0371f](https://levelup.gitconnected.com/visualizing-designing-and-analyzing-the-merge-sort-algorithm-cf17e3f0371f)

# 2. 복잡도

- 시간 복잡도 : 데이터의 분포에 상관 없이 O(nlogn)으로 동일함.
    - 왜냐하면 어떤 경우에도 무조건 반으로 계속해서 나눠가기 때문임.
- 공간 복잡도 : 두 개의 정렬된 리스트를 합병하는 과정에서 배열을 사용하기에 Linked List를 사용한다면 O(n)만큼의 공간이 필요함

# 3. 코드

```kotlin
fun mergeSort(array: MutableList<Int>, start: Int, end: Int) {
    if (start >= end) return

    val mid = (start + end) / 2
    mergeSort(array, start, mid)
    mergeSort(array, mid + 1, end)

    merge(array, start, mid, end)
}

fun merge(array: MutableList<Int>, start: Int, mid:Int, end: Int) {
    val newList = mutableListOf<Int>()
    var idxA = start
    var idxB = mid + 1

    while (idxA <= mid && idxB <= end) {
        if (array[idxA] <= array[idxB]) {
            newList.add(array[idxA])
            idxA++
        } else {
            newList.add(array[idxB])
            idxB++
        }
    }

    if (idxA > mid) {
        for (i in idxB..end) {
            newList.add(array[i])
        }
    }

    if (idxB > end) {
        for (i in idxA..mid) {
            newList.add(array[i])
        }
    }

    for (e in newList.indices) {
        array[start + e] = newList[e]
    }
}
```
