# 📍 퀵 정렬 (Quick Sort)

![quick-sort-001](https://user-images.githubusercontent.com/78673570/187065908-cb246f9b-94d8-423a-89da-56bddf71ca37.gif)

`분할 정복(divide and conquer)`을 통해 주어진 배열을 정렬

<br>

💡 분할 정복

1. Divide : 문제가 분할이 가능한 경우, 2개 이상의 문제로 나눈다.
2. Conquer : 나누어진 문제가 여전히 분할이 가능하면, 또 다시 Divide를 수행한다. 그렇지 않으면 문제를 푼다.
3. Combine : Conquer한 문제들을 통합하여 원래 문제의 답을 얻는다.

<br>

## 장점

- 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문에, 시간 복잡도가 O(nlogn)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
- 제자리 정렬의 일종으로 다른 메모리 공간을 필요로 하지 않는다.

<br>

## 단점

- 불안정 정렬이다.
- 정렬된 배열에 대해서는 Quick Sort의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.

<br>

## 구현

```java
void quickSort(int[] array, int left, int right) {
    if (left >= right) return;
    
    //분할
    int pivot = partition();

    //정복
    quickSort(array, left, pivot - 1);
    quickSort(array, pivot + 1, right);
}

int partition(int[] array, int left, int right) {
    int pivot = array[left];
    int i = left, j = right;

    while (i < j) {
        while (pivot < array[j]) i--;
        while (i < j && pivot >= array[i]) i++;
        swap(array, i, j);
    }
    array[left] = array[i];
    array[i] = pivot;

    return i;
}
```
