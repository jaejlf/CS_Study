# 삽입 정렬(Insertion Sort)

> 2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입 하여 정렬하는 알고리즘

<br>

<img src="https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/insertion-sort-001.gif">

<br>

### 특징

- **장점**
  - 안정한 정렬(Stable Sort) 방법
  - 레코드의 수가 적을 경우 알고리즘 자체가 매우 간단하므로 다른 복잡한 정렬 방법보다 유리할 수 있다.
  - 대부분위 레코드가 이미 정렬되어 있는 경우에 매우 효율적일 수 있다.
  - 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. <br>=> 제자리 정렬(in-place sorting)
- **단점**
  - 비교적 많은 레코드들의 이동을 포함한다.
  - 레코드 수가 많고 레코드 크기가 클 경우에 적합하지 않다.

### 삽입 정렬의 시간 복잡도

- Best: `O(n)`
  - 모두 정렬이 되어 있을 경우(Optimal), 한 번씩 밖에 비교하면 되므로
- Average: `O(n^2)`
- worst: `O(n^2)`

<br>

### 삽입 정렬의 공간 복잡도

- 주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 `O(n)` 이다.

<br>

### Psuedo Code

```Swift
for i from 1 to N
   key = a[i]
   j = i - 1
   while j >= 0 and a[j] > key
      a[j+1] = a[j]
      j = j - 1
   a[j+1] = key
```

<br>

### Insertion Sort in Swift

```Swift
func insertionSort(_ array: [Int]) -> [Int] {
    var arr = array
    for x in 1..<arr.count {
        var y = x
        while y > 0 && arr[y] < arr[y - 1] {
            swap(&arr[y - 1], &arr[y])
            y -= 1
        }
    }
    return arr
}
```
