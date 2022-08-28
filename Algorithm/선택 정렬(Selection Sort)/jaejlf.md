# 📍 선택 정렬 (Selection Sort)

![selection-sort-001](https://user-images.githubusercontent.com/78673570/187065398-baf0b512-c8f6-4fc2-8e72-a793e6619633.gif)

해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘

<br>

## 장점

- 알고리즘이 단순하다.
- 정렬을 위한 비교 횟수는 많지만 Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에, 많은 교환이 일어나야 하는 자료 상태에서 비교적 효율적이다.
- 제자리 정렬의 일종으로 다른 메모리 공간을 필요로 하지 않는다.

<br>

## 단점

- 시간복잡도가 O(n^2)으로 비효율적이다.
- 불안정 정렬이다.

<br>

## 구현

```java
void selectionSort(int[] arr) {
    int indexMin, tmp;
    for (int i = 0; i < arr.length - 1; i++) {
        indexMin = i;
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[indexMin]) {
                indexMin = j;
            }
        }
        tmp = arr[indexMin];
        arr[indexMin] = arr[i];
        arr[i] = tmp;
    }
    System.out.println(Arrays.toString(arr));
}
```
