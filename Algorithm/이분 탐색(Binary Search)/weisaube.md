# 이분 탐색(Binary Search)

## 📌 A. 이분 탐색(Binary Search)

<br/>

> 정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법

<br>

- 배열 내부의 데이터가 정렬되어 있어야지만 사용 가능한 알고리즘
- 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는 것

<br/>

<p align="center">
  <img src="https://blog.penjee.com/wp-content/uploads/2015/04/binary-and-linear-search-animations.gif" alt="text" width="485" />
</p>

<br/>

### Divide and Conquer

<br/>

#### 이분 탐색 원리

리스트의 중간 값과 비교하여 검색 값을 찾는다.
(중간값을 찾아야 하기 때문에 반드시 정렬된 배열에서만 사용 가능하다.)

1. 배열의 중간 값을 가져온다.
2. 중간 값과 검색 값을 비교한다.
   - 중간 값이 검색 값과 같다면 종료한다. (mid = key)
   - 중간 값보다 검색 값이 크다면 중간값 기준 배열의 오른쪽 구간을 대상으로 탐색한다. (mid < key)
   - 중간 값보다 검색 값이 작다면 중간값 기준 배열의 왼쪽 구간을 대상으로 탐색한다. (mid > key)
3. 값을 찾거나 간격이 비어있을 때까지 반복한다.

<br>

### 시간복잡도

<br/>

| operation | Best   | Average   | worst     |
| --------- | ------ | --------- | --------- |
| Search    | `O(1)` | `O(logN)` | `O(logN)` |

<br/>

### 종료 조건

<br/>

1. 검색 성공 시

   - 리스트에서 검색할 값과 같은 요소를 발견한 경우
   - `a[mid] == key`

2. 검색 실패 시
   - 더 이상 검색할 범위가 없는 경우
   - low > high

<br/>

### middle index 계산 과정

<br/>

```Swift
let mid: Int = low + (high - low) / 2
```

<br/>

lower index와 higher index를 더한 다음 2로 나누는 방식을 사용하지 않는 이유

- lower index와 Higher index가 `Integer`의 최대값을 벗어날 수 있기 때문에
- 그렇게 되면 overflow가 발생해서 값이 음수가 되고, 그 경우 array의 index를 벗어나게 된다.

그렇기 때문에 위의 방법으로 middle index를 구하는 것이 안전하다.

<br/>

## 📌 B. 구현

재귀로 구현하는 방법과 반복문으로 구현하는 방법이 있다.
(코드 출처는 SwiftAlgorithmClub)

<br/>

```Swift
func binarySearch(_ array: [Int], key: Int) -> Int? {
    var lowerBound = 0
    var upperBound = array.count
    while lowerBound < upperBound {
        let midIndex = lowerBound + (upperBound - lowerBound) / 2
        if a[midIndex] == key {
            return midIndex
        } else if a[midIndex] < key {
            lowerBound = midIndex + 1
        } else {
            upperBound = midIndex
        }
    }
    return nil
}
```

<br/>

## 📌 C. 참고자료

🔗 [[알고리즘] 이분 탐색 / 이진 탐색 (Binary Search)](https://velog.io/@kimdukbae/%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search)

🔗 [이진 탐색 (Binary search) 개념 및 구현](https://yoongrammer.tistory.com/75)
