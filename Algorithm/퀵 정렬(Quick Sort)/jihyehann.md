# 💡 퀵 정렬 (Quick Sort)

퀵 정렬은 합병 정렬(Merge sort)와 같이 `분할 정복(Divide and Conquer)` 알고리즘이다.

**배열의 요소 중 하나를 피벗(pivot)으로 선택하고, 피벗 주위에 지정된 배열을 분할**하여 정렬한다. 

피벗을 선택하는 방법에 따라 다양한 버전의 퀵 정렬이 있다.
- 첫 번째 원소를 피벗으로 정하는 방식 _(아래 구현은 이 방식이다)_
- 마지막 원소를 피벗으로 정하는 방식
- 임의의(random) 원소를 피벗으로 정하는 방식
- 중앙에 있는 원소를 피벗으로 정하는 방식

<br/>


## 1. 알고리즘

1. 배열 원소 중 하나를 골라 피벗으로 정한다.
2. 피벗보다 값이 작은 그룹과 큰 그룹으로 나눈다. (분할, Divide)
3. 분할이 완료되면 피벗을 작은 그룹과 큰 그룹 사이로 옮긴다.
4. 분할된 2개의 그룹에 대해 위의 과정을 재귀적으로 적용하여, 원소가 1개가 되어 더 이상 분할이 불가능해질 때까지 반복한다.

<br/>

![](https://velog.velcdn.com/images/wisdom-one/post/275e4112-797c-4d3a-9359-9f42731ccdf7/image.gif)

<br/>

## 2. 구현 (오름차순)
### Java
```java
static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
  
public void quickSort(int[] array, int left, int right) {
    if(left >= right) return;
    
    // 분할 
    int pivot = partition(); 
    
    // 피벗을 제외한 2개의 부분 배열을 대상으로 재귀 호출
    quickSort(array, left, pivot-1);  // 정복(Conquer)
    quickSort(array, pivot+1, right); // 정복(Conquer)
}


public int partition(int[] array, int left, int right) {
    /**
    // 최악의 경우, 개선 방법
    int mid = (left + right) / 2;
    swap(array, left, mid);
    */
    
    int pivot = array[left]; // 가장 왼쪽값을 피벗으로 설정
    int i = left, j = right;
    
    while(i < j) {
        while(pivot < array[j]) {
            j--;
        }
        while(i < j && pivot >= array[i]){
            i++;
        }
        swap(array, i, j);
    }
    array[left] = array[i];
    array[i] = pivot;
    
    return i; // 피벗 인덱스를 반환
}
```

<br/>

### 🔖 3-Way Quick Sort

퀵 정렬에서는 보통 피벗을 기준으로 2개의 그룹으로 분할하지만, 3개의 그룹으로 분할할 수도 있다. 

중복된 원소가 많은 배열인 경우, 다음과 같이 피벗을 기준으로 3개의 그룹으로 분할하는 것이 더 좋다.
- `arr[l..i]` : 피벗보다 작은 그룹
- `arr[i+1..j-1]` : 피벗과 값이 같은 그룹
- `arr[j..r]` : 피벗보다 큰 그룹

<br/>

<details markdown="1">
  <summary> 전체 구현 코드 </summary>

```java
static int i, j;

static void partition(int a[], int l, int r) {
   
    i = l - 1; j = r;
    int p = l - 1, q = r;
    int v = a[r]; // 마지막 원소를 피벗으로 정한다.
 
    while (true) {
       
        // 피벗 이상이 되는 첫 번째 원소를 찾는다.
        while (a[++i] < v)  ;
 
        // 피벗 이하가 되는 첫 번째 원소를 찾는다.
        while (v < a[--j])
            if (j == l)
                break;
 
        if (i >= j)
            break;
 
        // Swap
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
 
        // 피벗과 동일한 왼쪽 부분을 배열의 시작 부분으로 이동한다.
        if (a[i] == v) {
            p++;
            temp = a[i];
            a[i] = a[p];
            a[p] = temp;
        }
 
        // 피벗과 동일한 오른쪽 부분을 배열의 끝 부분으로 이동한다.
        if (a[j] == v) {
            q--;
            temp = a[q];
            a[q] = a[j];
            a[j] = temp;
        }
    }
 
    // 피벗을 올바른 인덱스로 이동
    int temp = a[i];
    a[i] = a[r];
    a[r] = temp;
   
    // 피벗과 동일한 왼쪽의 모든 원소를 시작부분부터 arr[i] 근처로 이동한다.
    j = i - 1;
    for (int k = l; k < p; k++, j--) {
        temp = a[k];
        a[k] = a[j];
        a[j] = temp;
    }
   
    // 피벗과 동일한 오른쪽의 모든 원소를 끝부분부터 arr[i] 근처로 이동한다.
    i = i + 1;
    for (int k = r - 1; k > q; k--, i++) {
        temp = a[i];
        a[i] = a[k];
        a[k] = temp;
    }
}
 
// 3개로 분할
static void quicksort(int a[], int l, int r) {
    if (r <= l)
        return;
 
    i = 0; j = 0;
 
    partition(a, l, r);
    
    quicksort(a, l, j);
    quicksort(a, i, r);
}
```
</details>
    
<br/>
  

## 3. 시간복잡도

### 1) best case : $O(nlog{_2}n)$

최선의 경우는 항상 중앙값으로 분할하는 경우다. 즉 분할 결과 양쪽의 원소 개수가 고르게 나눠진 경우를 말한다.

<br/>

<img src="https://velog.velcdn.com/images/wisdom-one/post/e5601100-5a14-4900-840e-3bf5ccd0c48b/image.png" width="80%"/>

<br/>

<p><div>이때 분할하는 데 걸리는 시간(비교 횟수)은 $O(n)$ 이고, 분할 단계는  $log{_2}n$ 개다.</div></p>

<p><div>따라서 시간복잡도는 $O(n) * log{_2}n = O(nlog{_2}n)$ 이다.</div></p>

<br/>

### 2) average case : $O(nlog{_2}n)$

<br/>

### 3) worst case : $O(n^2)$

최악의 경우는 분할한 결과가 한쪽으로만 몰리는 경우이다. 
이 경우는 이미 배열이 오름차순 혹은 내림차순으로 정렬되어 있는 경우다.

<br/>
<img src="https://velog.velcdn.com/images/wisdom-one/post/284be24c-a60f-4c4b-acdc-9985587f586e/image.png" width="40%"/>
<br/>
<p><div>이 때 분할하는데 걸리는 시간은 $O(n)$으로 같지만,  분할된 단계는 <b>n개</b>가 된다.</div></p>

<p><div>따라서 시간복잡도는 $O(n) * n = O(n^2)$ 이다.</div></p>

<br/>

## 4. 공간복잡도
재귀 함수 호출을 저장하기 위해 공간을 사용할 뿐, 추가적인 자료구조를 사용하지는 않으므로 in-place 알고리즘이다.

<p><div>Auxiliary Space (보조 공간) : $O(1)$</div></p>

<br/>

## 5. 장점
- <div>불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문에, <br/>
    시간복잡도가 $O(nlog{_2}n)$ 인 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.</div>
  
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. (in-place sorting)

<br/>

## 6. 단점
- 불안정 정렬(Unstable Sort) 이다.

- 정렬된 배열에 대해서는 Quick Sort의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.

<br/>

## 🔖 참고
- https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/%ED%80%B5%20%EC%A0%95%EB%A0%AC%20(Quick%20Sort).md
- https://www.geeksforgeeks.org/quick-sort/?ref=lbp
