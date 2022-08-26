# 💡 거품 정렬 (Bubble Sort)


거품 정렬 (Bubble Sort)이란, **서로 인접한 두 원소를 검사**하여 정렬하는 알고리즘이다.

<br/> 

`stable` sort이고, `In-place` 알고리즘이다.

> #### 🔖 Stable Sort (안정 정렬)
> 정렬을 했을 때 중복된 값들의 순서가 변하지 않는 정렬을 말한다.
> 
> #### 🔖 In-place Algorithm
> 원소들의 개수에 비해서 충분히 무시할 만한 저장 공간만을 더 사용하는 알고리즘을 말한다.
> 즉, 추가적인 메모리 공간이 거의 안 드는 알고리즘이다. 


<br/> 

## 1. 알고리즘

오름차순 정렬일 경우 다음과 같다.

1. 가장 왼쪽의 인접한 두 수를 비교하여 왼쪽 수가 오른쪽 수보다 더 크면 위치를 교환한다.
2. 오른쪽으로 1칸 이동하면서 같은 방식으로 두 수를 비교하여 교환하고, 가장 오른쪽에 도달할 때까지 이 과정을 반복한다. (결국 최댓값이 오른쪽 끝에 도착하게 된다.)
3. 오른쪽 끝에 최댓값이 도달하였음으로 이 원소를 제외하고, 나머지 원소에 대해서 비교 대상 원소가 1개가 남을 때까지 1번 과정부터 반복한다.
<br/> 

![](https://velog.velcdn.com/images/wisdom-one/post/a9f068fb-9b86-488d-a2d4-972c554f7d0b/image.gif)


<br/> 

## 2. 구현 

다음은 오름차순 정렬에 대한 구현 코드이다.

### 구현 코드
#### Java

```java
void bubbleSort(int[] arr) {
    int temp = 0;
    for(int i = 0; i < arr.length; i++) {
        for(int j = 1 ; j < arr.length-i; j++) {
            if(arr[j-1] > arr[j]) {
                // swap(arr[j-1], arr[j])
                temp = arr[j-1];
                arr[j-1] = arr[j];
                arr[j] = temp;
            }
        }
    }
}
```
<br/> 

### 최적화된 구현 코드
- 버블 소트는 정렬이 완료된 배열에서도 계속해서 알고리즘을 수행한다.
즉, 항상 시간복잡도가 O(n^2) 이다.
- `최적화된 버블 소트`는 내부 loop에서 swap이 발생하지 않으면, 정렬이 완료된 것으로 보고 알고리즘을 멈춘다.


#### Java
```java
void bubbleSort(int arr[], int n) {
    int i, j, temp;
    boolean swapped;
    for (i = 0; i < n - 1; i++) {
        swapped = false;
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // swap arr[j] and arr[j+1]
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true; // swap 발생
            }
        }

        // swap이 발생하지 않았으면, break 
        if (swapped == false)
            break;
    }
}
```

<br/> 

## 3. 시간복잡도

### 일반 구현 코드

항상 O(n^2) 이다.

- 비교 횟수 : (n-1) + (n-2) + (n-3) + ... + 2 + 1 = n(n-1)/2

- 교환 횟수 : 0 ~ n(n-1)/2

<br/> 

### 최적화된 구현 코드

- **Worst Case** (반대로 정렬된 경우) : O(n^2)

  - 비교 횟수 : n(n-1)/2
  
  - 교환 횟수 : n(n-1)/2
  
- **Average Case** : O(n^2)
 
  
- **Best Case** (이미 정렬된 경우) : O(n)
  - 비교 횟수 : n-1
  
  - 교환 횟수 : 0

<br/> 

## 4. 공간복잡도

버블 소트는 다른 자료구조 없이, 인접한 두 개의 값만 비교하여 교환하기 때문에 In-place 알고리즘이다.

Auxiliary Space (보조 공간) : O(1)

<br/> 

## 5. 장점
- 구현이 매우 간단하고, 소스코드가 직관적이다.
- 정렬하고자하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않다.(in-place sorting)
- 안정 정렬(Stable Sort) 이다.

<br/> 

## 6. 단점
- 시간복잡도가 비효율적이다.
- 정렬되어 있지 않은 원소가 정렬된 자리로 가기 위해서, 교환 연산(swap)이 많이 발생한다.

<br/> 

## 7. 사용 용도
- 정렬 알고리즘의 개념을 도입하는 데 종종 사용된다.
- `컴퓨터 그래픽스`에서, 거의 정렬된 배열에서 작은 오류(ex.두 요소의 교환)를 감지할 때 선형 복잡도로 수정할 수 있어 많이 사용된다.

<br/> 

## 🔖 참고
- https://www.geeksforgeeks.org/bubble-sort/
- https://velog.io/@cookncoding/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%9C%EB%85%90-Stable-Sort-Inplace
