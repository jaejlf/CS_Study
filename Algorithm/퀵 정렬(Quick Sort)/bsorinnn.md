# 퀵 정렬(Quick Sort)

> 비교 정렬의 일부. 분할 정복(divide and conquer) 방법을 통해 리스트를 정렬

1. 리스트 가운데서 원소를 고른다 <br>
   => 이렇게 고른 원소를 **피벗(pivot)** 이라고 한다
2. 피벗 앞에서는 피벗보다 값이 작은 모든 원소를, 피벗 뒤에서는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 리스트를 둘로 나눈다.<br>
   => 이렇게 리스트를 둘로 나눈 것을 **분할**이라고 한다.
3. 분할된 작은 리스트에 대해 재귀적으로 이 과정을 반복한다.

재귀 호출이 한 번 진행될 때마다 최소한 하나의 원소는 최종적으로 위치가 정해진다.

<br>

**분할 정복(Divide and Conquer)로 보는 퀵 정렬**

- 분할(Divide): 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열(피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)로 분할한다.
- 정복(Conquer): 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출 을 이용하여 다시 분할 정복 방법을 적용한다.
- 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 합병한다.
  순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.

<br>

<img src="https://noah0316.github.io/static/4e3b740ec82525fad6b2c8399f75f86e/5d72a/7.png" height=200>

<br>

퀵 정렬에서는 좋은 기준(pivot)을 선택하는 것이 중요하다.<br>

대표적인 피벗을 선택하는 방식은 다음과 같다

**피벗 선택 방법**

- 랜덤 방식:
  - 임의의 위치를 선택하여 pivot으로 선정
  - 최악의 확률은 줄어드나, 확률에 따라 실행마다 크게 달라질 수 있다
- middle index 방식:
  - 배열의 중간 위치 선택 (len(array)/2) -**정렬된** 경우에 최악을 피하기 위해
  - 일반적인 분포(마지막, 첫번째 값이 중간값일 경우)에 취약할 수 있다
- median 방식:
  - 중간 값을 선택
  - 대부분 경우 최악의 값을 피할 수 있다

<br>

### 특징

- **장점**
  - 속도가 빠르다
  - 추가 메모리 공간을 필요로 하지 않는다.
- **단점**
  - 정렬된 리스트에 대해서는 퀵 정렬의 불균
  - 퀵 정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택

<br>

### 퀵 정렬의 시간복잡도

- Best: `O(nlogn)`
- Average: `O(nlogn)`
- Worst: `O(n^2)`

<br>

## B. 퀵 정렬 Swift로 구현하기

<br>

```Swift


func quickSort(_ array: [Int]) -> [Int] {
    guard array.count > 1 else { return array }

    // 여기서는 middle index 방식
    let pivot = array[array.count / 2]
    let less = array.filter { $0 < pivot }
    let equal = array.filter { $0 == pivot }
    let greater = array.filter { $0 > pivot }

    return quickSort(less) + equal + quickSort(greater)
}
```
