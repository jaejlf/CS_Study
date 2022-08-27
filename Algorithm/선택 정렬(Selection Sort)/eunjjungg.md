# 1. 선택 정렬

> Bubble sort와 같은 제자리 정렬 알고리즘 (in-place sorting, 입력 배열 이외에 다른 추가 메모리 공간을 요구하지 않는 정렬 방법)
> 

<br/>

**알고리즘**

1. 첫 번째 자료를 두 번째부터 마지막 자료까지 순차적으로 비교하여 가장 작은 값을 첫 번째에 놓음 그리고 그 위치에 첫 번째 자료였던 값이 감
2. 1번을 완료하면 가장 작은 자료가 첫 번째에 자리하게 되므로 두 번째자료를 기준으로 세 번째부터 마지막 자료까지 순차적으로 비교하여 가장 작은 값을 두 번째 자리에 놓음 그리고 그 위치에 두 번째 자료였던 값이 감
3. 3…n-1번째 자료에 대해서도 동일하게 적용

<br/>

![image](https://user-images.githubusercontent.com/100047095/187008237-2335ffab-bcf1-45c4-8f99-807c3c87a73c.png)
출처 : [https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)

<br/><br/>

# 2. 복잡도

| best | avg | worst |
| --- | --- | --- |
| n^2 | n^2 | n^2 |

아래의 코드를 보면 알 수 있듯 루프가 두 개이므로 O(n^2)를 만족함

<br/><br/>

# 3. code

```kotlin
var min: Int
// 마지막 값은 정렬할 필요 없으므로 0 until n - 1
for (i in 0 until n - 1) {
    // 초기 index를 최솟값 index로 설정
    min = i
    // 초기 index의 다음 index부터 마지막 index까지 순회
    for (j in i+1 until n) {
        // 값 비교 후 mininum index 변경
        if (array[min] > array[j]) min = j
    }
    // 최솟값을 앞에 배치
    swap(array, i, min)
}
```
