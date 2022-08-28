# 📍 삽입 정렬 (Insertion Sort)

![insertion-sort-001](https://user-images.githubusercontent.com/78673570/187065102-5c476e81-cb50-4f0c-8e78-bcb8c0062c9a.gif)

2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬하는 알고리즘

<br>

## 장점

- 알고리즘이 단순하다.
- 대부분의 원소가 이미 정렬되어 있는 경우 매우 효율적이다.
- 제자리 정렬의 일종으로 다른 메모리 공간을 필요로 하지 않는다.
- Selection Sort나 Bubble Sort와 같은 O(n^2) 알고리즘과 비교하여 상대적으로 빠르다.
- 안정 정렬이므로 중복된 값이 입력 순서와 동일하게 정렬된다.

<br>

## 단점

- 평균과 최악의 시간복잡도가 O(n^2)으로 비효율적입니다.
- 배열의 길이가 길어질수록 비효율적이다.

<br>

## 구현

```java
void insertionSort(int[] arr) {
    for (int index = 1; index < arr.length; index++) {
        int tmp = arr[index];
        int prev = index - 1;
        while ((prev >= 0) && (arr[prev] > tmp)) {
            arr[prev + 1] = arr[prev];
            prev--;
        }
        arr[prev + 1] = tmp;  
    }
    System.out.println(Arrays.toString(arr));
}
```
