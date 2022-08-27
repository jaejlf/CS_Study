# 1. 퀵 정렬, quick sort

> divide-conquer 방식 : 문제를 작은 두 개의 문제로 분리하고 각각을 해결한 뒤 결과를 모아 원래의 문제를 해결하는 방식
> 

<br/>

**알고리즘**

1. 정렬할 리스트 안의 한 요소를 선택 → pivot
2. pivot을 기준으로 pivot 보다 작은 요소들은 모두 pivot의 왼쪽, 큰 요소들은 pivot의 오른쪽으로 옮겨짐
3. pivot을 제외한 왼쪽 리스트, 오른쪽 리스트를 대상으로 다시 1, 2를 반복 (divide-conquer)
4. 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복함

<br/>

**Divide & Conquer in Quick Sort**

- Divide : 입력 배열을 피봇을 기준으로 비균등하게 두 개의 부분 배열로 분할함
- Conquer : 부분 배열을 정렬함, 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용해서 다시 divide & conquer 방식을 적용
- Combine : 정렬된 부분 배열들을 다시 하나의 배열에 합병함

<br/>

![image](https://user-images.githubusercontent.com/100047095/187008996-8d77406f-6df4-4c27-b215-bd6f332781fb.png)
출처 : [https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)

<br/><br/>

# 2. 복잡도

**공간 복잡도**

O(log n) (최악의 경우 O(n))

<br/>

**시간 복잡도**

| bset | avg | worst |
| --- | --- | --- |
| nlogn | nlogn | n^2 |

worst case : 완전 정렬된 경우에서 pivot이 가장 크거나 가장 작은 값을 가진 값이 선정되는 경우 왼쪽 혹은 오른쪽 리스트에 값이 모두 몰리게 되어 최악의 경우가 됨 

<br/>

# 3. code

```kotlin
fun quickMerge(arr: ArrayList<Int>): ArrayList<Int> {

    if (arr.size <= 1) return arr

    // index의 처음 값 pivot 설정
    val pivot = arr.removeFirst()

    val left = arrayListOf<Int>()
    val right = arrayListOf<Int>()

    for (i in arr.indices) {

        // pivot과 배열의 각 값 비교하여 left or right 배열에 추가
        if (arr[i] > pivot) {
            right.add(arr[i])
        } else {
            left.add(arr[i])
        }
    }

    val mergedList = arrayListOf<Int>()

    // 재귀함수를 통해 정렬된 left, right 배열 left + pivot + right 순으로 merge
    mergedList.addAll(quickMerge(left))
    mergedList.add(pivot)
    mergedList.addAll(quickMerge(right))
    return mergedList
}
```
