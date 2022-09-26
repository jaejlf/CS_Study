# 💡 합병 정렬 (Merge Sort)

`분할 정복(Divide and Conquer)` 알고리즘으로, 안정 정렬(stable sort) 이다.

## 1. 알고리즘

1. 배열을 반으로 나눈다.
2. 부분 배열에 대하여, 더 이상 분할할 수 없을 때까지 1번을 반복한다.
3. 분할이 완료된 후, 이웃하는 서브배열을 병합하여 정렬을 완료한다.

<br/>

![merge sort](https://user-images.githubusercontent.com/75151848/192196023-bad9a7db-c275-42c1-a59b-672977119e24.gif)

<br/>

## 2. 구현 (오름차순)
### Java
```java
// 2개의 부분 배열 정렬 및 병합
public void merge(int arr[], int l, int m, int r) {
    // 부분 배열의 크기 계산
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[] = new int[n1];
    int R[] = new int[n2];
    
    for (int i = 0; i < n1; ++i)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; ++j)
        R[j] = arr[m + 1 + j];

    // 부분 배열의 인덱스 i,j
    int i = 0, j = 0;

    // merge된 인덱스 k
    int k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        }
        else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    /* L[]의 남아있는 원소 복사 */
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    /* R[]의 남아있는 원소 복사 */
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// merge sort 메인 함수
public void sort(int arr[], int l, int r) {
    if (l < r) { // 배열의 크기가 2 이상일 때 수행
        
        // 분할
        int m = l + (r - l) / 2;
        
        sort(arr, l, m);     // 정복
        sort(arr, m + 1, r); // 정복

        // 2개의 부분 배열 합병
        merge(arr, l, m, r);
    }
}
```

<br/>

## 3. 시간복잡도

항상 $O(nlogn)$ 의 시간 복잡도를 가진다.

<img src="https://user-images.githubusercontent.com/75151848/192196765-721cd2a0-80c8-47a6-b995-7efffcf0065a.png"
     width="80%"/>

- 비교 횟수 : 분할 단계 * 합병 시 최대 비교 횟수 = $log_{2}n * n$ = $nlog_{2}n$
- 이동 횟수 : 분할 단계 * 합병 시 이동 횟수 = $log_{2}n * 2n$ = $2nlog_{2}n$
- 따라서, $T(n) = nlog_{2}n + 2nlog_{2}n = O(nlogn)$


<br/>

## 4. 공간복잡도

합병 정렬은 모든 원소들이 보조 배열에 복사된다. (in-place 알고리즘이 아니다.)

Auxiliary Space (보조 공간) : $O(n)$

<br/>

## 5. 장점

- 안정 정렬(stable sort) 이다.
- 데이터의 분포에 영향을 덜 받으며, 입력 데이터가 무엇이든 정렬되는 시간은 동일하다. (O(nlog₂n)로 동일)
- 레코드를 연결 리스트(Linked List)로 구성하면, <br/>
    링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아지고, 제자리 정렬(in-place sorting)로 구현할 수 있다.
- 크기가 큰 레코드를 정렬할 경우에 연결 리스트를 사용한다면, 합병 정렬은 퀵 정렬을 포함한 다른 어떤 졍렬 방법보다 효율적이다.

 > 🔖 참고. [Merge two sorted lists (in-place)](https://www.geeksforgeeks.org/merge-two-sorted-lists-place/)

<br/>

## 6. 단점

- 제자리 정렬(in-place sorting)이 아니다. <br/>
  레코드를 배열(Array)로 구성하면, 임시 배열이 필요하다.
- 레크드들의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래한다.

<br/>

## 🔖 참고
- https://www.geeksforgeeks.org/merge-sort/?ref=lbp
- https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
