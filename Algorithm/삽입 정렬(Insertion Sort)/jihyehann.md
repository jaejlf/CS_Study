# 💡 삽입 정렬(Insertion Sort)	

삽입 정렬은 **2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입**하여 정렬하는 알고리즘이다.

손으로 카드를 정렬하는 방법과 유사하다.

<br/>

## 1. 알고리즘

1. 리스트의 첫 번째 위치의 값은 이미 정렬이 완료된 리스트다.
2. 정렬 리스트의 오른쪽에 있는 정렬되지 않은 원소를 왼쪽으로 이동하면서 원소들과 비교하여 삽입한다.
3. 이 과정을 정렬되지 않은 원소가 없을 때까지 반복한다.

![](https://velog.velcdn.com/images/wisdom-one/post/af7786a7-9dad-4a25-aff8-214f3c911a0f/image.gif)


<br/>

## 2. 구현 (오름차순)

### Java
```java
void insertionSort(int arr[]) {
    int n = arr.length;
    for (int i = 1; i < n; ++i) { // 두 번째 원소부터 탐색한다.
        int key = arr[i];
        int j = i - 1;

        // key보다 큰 원소를 한 위치씩 뒤로 보낸다.
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        // 삽입
        arr[j + 1] = key;
    }
}
```


<br/>

## 3. 시간복잡도
<p><div><b>Worst Case</b> (반대로 정렬된 경우) : $O(n^2)$ </div></p>

<p><div><b>Average Case</b> : $O(n^2)$ </div></p>

<p><div><b>Best Case</b> (이미 정렬된 경우) : $O(n)$ </div></p>

<br/>

## 4. 공간복잡도
in-place 알고리즘으로, 추가적인 자료구조를 사용하지 않는다.

<p><div>Auxiliary Space (보조 공간) : $O(1)$ </div></p>

<br/>

## 5. 장점
- 알고리즘이 단순하다.
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. (in-place sorting)
- 안정 정렬(Stable Sort)이다.
- Selection Sort나 Bubble Sort과 같은 $O(n^2)$ 알고리즘에 비교하여 상대적으로 빠르다.

<br/>

## 6. 단점
- 평균과 최악의 시간복잡도가 $O(n^2)$으로 비효율적이다.
- Bubble Sort와 Selection Sort와 마찬가지로, 배열의 길이가 길어질수록 비효율적이다.

<br/>

## 🔖 참고
- https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/%EC%82%BD%EC%9E%85%20%EC%A0%95%EB%A0%AC%20(Insertion%20Sort).md
- https://www.geeksforgeeks.org/insertion-sort/?ref=lbp
