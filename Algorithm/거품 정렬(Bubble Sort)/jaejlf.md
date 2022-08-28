# 📍 거품 정렬 (Bubble Sort)

![image](https://user-images.githubusercontent.com/78673570/187064732-15a7be02-3851-4670-b298-0c9be9d7707e.gif)

서로 인접한 두 원소의 크기를 비교하고, 조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘

<br>

## 장점

- 구현이 간단하고, 코드가 직관적이다.
- 제자리 정렬이므로 공간복잡도가 O(n)이다.
- 안정 정렬이므로 중복된 값이 입력 순서와 동일하게 정렬된다.

<br>

## 단점

- 시간복잡도가 최악/최선/평균 모두 O(n^2)으로 매우 비효율적이다.
- 특정 요소가 최종 정렬 위치에 있는 경우라도 교환이 일어난다.
- 일반적으로 자료의 교환(swap) 작업이 이동(move) 작업보다 더 복잡하다.


<br>

## 구현

```java
void bubbleSort(int[] arr) {
    int tmp = 0;
    for (int i = 0; i < arr.length; i++) {
        for (int j = 1; j < arr.length - i; j++) {
            if (arr[j - 1] > arr[j]) {
                tmp = arr[j - 1];
                arr[j - 1] = arr[j];
                arr[j] = tmp;
            }
        }
    }
    System.out.println(Arrays.toString(arr));
}
```
