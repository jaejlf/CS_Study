# 1. 삽입 정렬, insertion sort

> 처음 key 값이 두 번째 자료부터 시작하는 알고리즘

<br/>

**알고리즘**

1. 두 번째 자료부터 시작하여 그 앞의 자료들과 비교하여 삽입할 위치를 지정한 뒤 자료를 해당 자리로 옮김
2. 세 번째 자료는 첫 번째와 두 번째 자료 사이의 대소를 비교하여 삽입할 위치를 지정한 뒤 자료를 해당 자리로 옮김
3. 4…n번째 자료에 대해서도 동일한 작업 수행

<br/>

![image](https://user-images.githubusercontent.com/100047095/187008526-a2ade156-6d33-4594-bb4c-a4b411139ee5.png)

출처 : [https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)

<br/><br/>

# 2. 복잡도

| best | avg | worst |
| --- | --- | --- |
| n | n^2 | n^2 |

best case : 이동 없이 1 번의 비교만 이루어지는 경우 (정렬된 경우)

worst case : 입력 자료가 역순으로 정렬된 경우 모든 for 문을 다 돌아야 하므로 O(n^2)가 됨 

<br/>

# 3. 코드

```kotlin
// 첫번째 값은 삽입의 대상이 아니므로 0 until n-1
for (i in 0 until n - 1) {
    // i + 1 번째 값에 대해 삽입 대상으로 지정
    for (j in i + 1 downTo 1) {
        // j - 1 값과 비교하며 더 작을 시 앞 index로 이동
        if (array[j] < array[j - 1]) swap(array, j, j - 1)
        // j - 1이 더 작을 시 비교 종료
        else break
    }
}
```
