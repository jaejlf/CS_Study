# 병합정렬 (Merge Sort)

## A. 병합 정렬(=합병 정렬)이란?

> 둘 이상의 부분집합으로 나눈 후, 각 부분집합들을 정렬하여 부분집합들끼리 다시 정렬된 형태로 합치는 방식

<br/>

- `분할 정복 방식(Divide and Conquer)`으로 설계된 알고리즘
  - 두 개의 배열로 계속 쪼개어 나간 뒤, 합치면서 정렬
- 시간복잡도: O(n log n)
- 분할 과정: N → N/2 2개 → N/4 4개 ... : logN 만큼 반복해야 크기가 1인 배열로 분할됨
  - 각 분할별로 합병을 진행하기 때문에 NlongN
- 공간복잡도: O(N)
  - 정렬을 위한 배열을 하나 더 생성하기 때문에 2N개 사용

<br/>

<img src="https://i.imgur.com/HU2tfzo.gif">

<br/>

### 병합 정렬의 과정

- 분할(Divide): 입력 배열을 같은 크기의 2개의 부분 배열로 분할한다.
- 정복(Conquer): 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출 을 이용하여 다시 분할 정복 방법을 적용한다.
- 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 합병한다.

<br/>

### 특징

- 추가적인 리스트가 필요하다.
- 각 부분 배열을 정렬할 때도 합병 정렬을 순환적으로 호출하여 적용한다.
- 합병 정렬에서 실제로 정렬이 이루어지는 시점은 2개의 리스트를 합병(merge)하는 단계다.

<br/>

### 장단점

- 단점
  - 만약 레코드를 배열(Array)로 구성하면, 임시 배열이 필요하다.
  - 제자리 정렬(in-place sorting)이 아니다.
  - 레크드들의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래한다.
- 장점
  - 안정적인 정렬 방법
  - 데이터의 분포에 영향을 덜 받는다. 즉, 입력 데이터가 무엇이든 간에 정렬되는 시간은 동일하다. (O(nlog₂n)로 동일)

<br/>

### 병합 정렬 구현

```swift

func mergeSort(_ array: [Int]) -> [Int] {
  guard array.count > 1 else { return array }

  let middleIndex = array.count / 2

  let leftArray = mergeSort(Array(array[0..<middleIndex]))
  let rightArray = mergeSort(Array(array[middleIndex..<array.count]))

  // here
  return merge(leftArray, rightArray)
}

```

## B. 참고자료

🔗 https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
