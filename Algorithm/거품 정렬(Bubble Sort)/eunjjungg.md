# 1. 거품 정렬, Bubble Sort

> 서로 인접한 두 원소를 검사하여 정렬하는 알고리즘<br/>
→ 인접한 두 개의 레코드를 비교하여 크기가 순차적이지 않으면 서로 교환함<br/>
> 

<br/>

**알고리즘**

1. 1, 2번째 자료들을 비교하고 정렬하고 2, 3번째 자료를 비교하고 정렬하고… n-1, n번째 자료들을 비교하고 정렬한다
2. 1번을 수행하고 나면 가장 큰 자료가 가장 뒤로 이동하므로 비교를 다시 할 때는 맨 끝 자료(가장 큰 자료)는 정렬에서 제외하고 n-1개를 대상으로 1번을 다시 수행한다

<br/>

![image](https://user-images.githubusercontent.com/100047095/187007922-6517e97a-9691-4753-bca1-bb26381eee54.png)

출처 : [https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)

<br/><br/>

# 2. 복잡도

| best | avg | worst |
| --- | --- | --- |
| n^2 | n^2 | n^2 |

단순하지만 비효율적임 

<br/><br/>

# 3. code

```kotlin
// 바깥쪽 loop(배열을 순회할 횟수)
for (i in 0 until n - 1) {
    var isSwap = false
    // 안쪽 loop(swap 여부를 판단할 횟수)
    // 바깥쪽 loop가 한 번 돌 때마다 배열의 끝에 정렬된 값이 들어오므로 n - 1 - i
    for (j in 0 until n - 1 - i) {
        if (array[j] > array[j + 1]) {
            swap(array, j, j + 1)
            isSwap = true
        }
    }

    // 정렬이 완료된 경우 바로 return (시간복잡도 감소)
    if (!isSwap) {
        return
    }
}
```
