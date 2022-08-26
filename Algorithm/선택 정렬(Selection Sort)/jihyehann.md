# 💡 선택 정렬(Selection Sort)

Bubble Sort과 유사한 알고리즘으로, **해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택**하는 알고리즘이다.

<br/>

## 1. 알고리즘

이 알고리즘은 2가지 subarray를 가진다.
- 정렬이 완료된 subarray (앞부분)
- 아직 정렬하지 않은 subarray (뒷부분)


오름차순 정렬일 경우 다음과 같다.

1. 정렬이 완료되지 않은 부분에서 최솟값을 탐색한다.
2. 맨 앞 원소와 최솟값 원소를 교환한다.
3. 정렬된 원소를 제외한 나머지 원소에 대해 위 과정을 반복한다.

<br/>

<div style="text-align:center;"> 
  <div>worst case </div>
  <img src="https://velog.velcdn.com/images/wisdom-one/post/2bad37f2-f868-4f39-943a-4bfade569172/image.gif"/>
</div>

<div style="text-align:center;"> 
   <div>average case <div>
  <img src="https://velog.velcdn.com/images/wisdom-one/post/d4fba88a-177e-483c-a107-535302380c2d/image.gif"/>
</div>

<br/>
     
## 2. 구현

```java
void selectionSort(int arr[]) {
    int n = arr.length;

    // 정렬되지 않은 subarray에서 하나씩 비교
    for (int i = 0; i < n - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[min_idx])
                min_idx = j;

        // Swap
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}
```
                                      
<br/>
     
## 3. 시간복잡도

이중 루프를 사용하기 때문에 $O(n^2)$ 의 시간복잡도를 가진다 (best, average, worst case 모두 동일하다).
     
<ul>
  <li>위치 선택 : $O(n)$</li>
  <li> 최솟값(혹은 최댓값)을 찾기 위한 원소 비교 : $O(n)$</li>
</ul>
<div>&rarr; $O(n) * O(n)$ = $O(n*n)$ = $O(n^2)$</div>

<br/>

## 4. 공간복잡도

선택 정렬은 in-place 알고리즘으로, 추가적인 자료구조를 사용하지 않는다.

<div>Auxiliary Space (보조 공간) : $O(1)$</div>
     
<br/>

## 5. 장점
- Bubble sort와 마찬가지로 알고리즘이 단순하다.
- 정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적이다.
- Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않다. (in-place sorting)

<br/>

## 6. 단점
- 시간복잡도가 $O(n^2)$으로, 비효율적이다.
- 기본적으로 불안정 정렬(Unstable Sort)이다. &rarr; [[참고] stable sort로 만드는 방법](https://www.geeksforgeeks.org/stable-selection-sort/)

<br/>


## 🔖 참고
- https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/%EC%84%A0%ED%83%9D%20%EC%A0%95%EB%A0%AC%20(Selection%20Sort).md#%EC%84%A0%ED%83%9D-%EC%A0%95%EB%A0%AC-selection-sort
- https://www.geeksforgeeks.org/selection-sort/?ref=lbp
