# 📍 병합 정렬 (Merge Sort)

![image](https://user-images.githubusercontent.com/78673570/193421297-f8577f47-e4f8-4039-83a2-0dd9ce001857.png)

- `분할 정복(divide and conquer)`을 통해 주어진 배열을 정렬
- 정렬할 리스트를 반으로 쪼개나가며 → 좌측과 우측 리스트를 계속하여 분할해 나간 후 → 각 리스트내에서 정렬 후 → 병합하는 과정을 통해 정렬하는 알고리즘


<br>

💡 퀵 정렬과의 차이점
- 퀵 정렬 : 우선 피벗을 통해 정렬(partition) → 영역을 쪼갬(quickSort)
- 병합 정렬 : 영역을 쪼갤 수 있을 만큼 쪼갬(mergeSort) → 정렬(merge)

<br>

## 장점

- 최선의 경우에도, 최악의 경우에도 시간복잡도가 O(nlogn)이다.
- 안정 정렬이므로 중복된 값이 입력 순서와 동일하게 정렬된다.

<br>

## 단점

- 별도의 메모리 공간이 필요하다.

<br>

## 구현

```java
private void solve() {
    int[] array = {230, 10, 60, 550, 40, 220, 20};

    mergeSort(array, 0, array.length - 1);

    for (int v : array) {
        System.out.println(v);
    }
}

public static void mergeSort(int[] array, int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;

        mergeSort(array, left, mid);
        mergeSort(array, mid + 1, right);
        merge(array, left, mid, right);
    }
}

public static void merge(int[] array, int left, int mid, int right) {
    int[] L = Arrays.copyOfRange(array, left, mid + 1);
    int[] R = Arrays.copyOfRange(array, mid + 1, right + 1);

    int i = 0, j = 0, k = left;
    int ll = L.length, rl = R.length;

    while (i < ll && j < rl) {
        if (L[i] <= R[j]) {
            array[k] = L[i++];
        } else {
            array[k] = R[j++];
        }
        k++;
    }

    while (i < ll) {
        array[k++] = L[i++];
    }

    while (j < rl) {
        array[k++] = R[j++];
    }
}
```
