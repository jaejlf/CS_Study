# 버블 정렬(Bubble Sort)

> 서로 인접한 두 원소를 검사하여 정렬하는 알고리즘

<br>

<img src="https://cdn.programiz.com/cdn/farfuture/kn1zM7ZGIj60jcTe3mv8gAtbrvFHqxgqfQ7F9MdjPuA/mtime:1582112622/sites/tutorial2program/files/Bubble-sort-0.png" height=250>

<br>

- 서로 인접한 두 원소를 검사하여 정렬하는 알고리즘
  - 인접한 2개의 레코드를 비교하여 크기가 순서대로 되어 있지 않으면 서로 교환

### 특징

- **장점**
  - 구현이 매우 간단하다
- **단점**

  - 순서에 맞지 않은 요소를 인접한 요소와 교환한다.
  - 하나의 요소가 가장 왼쪽에서 가장 오른쪽으로 이동하기 위해서는 배열에서 모든 다른 요소들과 교환되어야 한다.
  - 특히 특정 요소가 최종 정렬 위치에 이미 있는 경우라도 교환되는 일이 일어난다.
  - 일반적으로 자료의 교환 작업(SWAP)이 자료의 이동 작업(MOVE)보다 더 복잡하기 때문에 버블 정렬은 단순성에도 불구하고 거의 쓰이지 않는다.

    <br>

### 버블 정렬의 시간 복잡도

- Best: `O(n^2)`
- Average: `O(n^2)`
- worst: `O(n^2)`

<br>

## B. 버블 정렬 Swift로 구현하기

<br>

#### Psudeo Code

```Swift
func bubblesort( var a as array )
    for i from 1 to N
        for j from 0 to N - 1
           if a[j] > a[j + 1]
              swap( a[j], a[j + 1] )
end func
```

<br>

```Swift
for i in 0..<array.count {
  for j in 1..<array.count - i {
    if array[j] < array[j-1] {
      let tmp = array[j-1]
      array[j-1] = array[j]
      array[j] = tmp
    }
  }
}
return array
```
