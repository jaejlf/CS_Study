# 1. 계수 정렬

> 비교 연산을 수행하지 않는 정렬<br/>
배열 내에 특정한 값이 몇번 등장하는지에 따라 정렬을 수행함.
> 

![image](https://user-images.githubusercontent.com/100047095/193398599-79d3fc7e-4d5c-4bee-86b2-6b8d26f1a3a6.png)
출처 : [https://8iggy.tistory.com/123](https://8iggy.tistory.com/123)

**알고리즘 요약**

1. 입력 받은 배열 A의 요소값들의 등장횟수를 저장할 배열 B와 최종적으로 정렬된 요소들을 담을 배열 C를 준비
2. 입력 받은 배열에서 값을 하나씩 꺼내서 해당 값을 배열 B의 인덱스 값으로 사용해 B의 요소를 증가시킴 (`B[A[i]]++`)
3. B가 완성되면 B의 각 요소들을 누적합으로 갱신함
4. A의 가장 뒤에서부터 값을 하나씩 꺼내 해당 값을 B의 인덱스로 사용하고 참조된 B의 값을 배열 C의 인덱스 값으로 사용해서 배열 C에 배열 A에서 꺼낸 값을 넣음 (`C[B[A[i]]] = A[i]`)
5. 사용된 B의 값을 하나 감소시킴 (`B[A[i]]--`)
6. A의 모든 요소에 대해 4, 5번을 반복

<br/><br/>

# 2. 복잡도

- 시간 복잡도 : O(n + k)
    - k : 정렬할 수들 중 가장 큰 값
    - n : 정렬할 수의 개수
    - 이론 (출처 : [https://8iggy.tistory.com/123](https://8iggy.tistory.com/123))
        
        정렬 과정을 살펴보면 만약 최대값이 주어지지 않은 경우 전체 배열을 탐색해야 하므로 O(n)이 소요되고, Counting Array에 개수를 count하는 과정도 O(n)이 소요된다. 이후 출력 배열에 값을 입력하여 정렬된 배열을 얻는 과정에도 O(n)이 소요된다. 따라서 시간 복잡도는 O(n)이 된다. 그러나, 배열의 길이와 상관없이 배열의 최댓값 K가 정렬 시간의 변수로 작용하며 배열의 길이가 작은데 K가 굉장히 클 경우(ex. [1, 10000]) 정렬 시간은 K에 종속된다. 따라서, 일반적으로 카운팅 정렬의 시간복잡도는 O(n+k)라고 말한다. 그리고 K가 최대한 작아야 유리하므로 입력값의 범위가 작을 때 높은 효율을 보인다.
        
- 공간 복잡도 : 가장 큰 숫자인 k의 값에 크게 영향을 받음

# 3. 코드

```kotlin
class CountingSort : SortAlgorithm {

    override fun sort(arr: Array<Long>): Array<Long> {
        val countsArray = Array<Int>(maximum(arr), { i -> 0})
        //Determining counts of every integer in input array
        for (i in 0..arr.size - 1){
            val countsArrayIndex = arr[i].toInt() - 1 //Counts array is indexed by the values from the input array
            countsArray[countsArrayIndex] = countsArray[countsArrayIndex] + 1
        }
        //Determining counts of integers smaller than current input array integer
        for (j in 1..countsArray.size - 1){
            countsArray[j] = countsArray[j] + countsArray[j - 1]
        }
        //Preparing sorted output array
        val outputArray = Array<Long>(arr.size, { i -> 0})
        var k = arr.size - 1
        while(k >= 0){
            val countsArrayIndex = arr[k].toInt() - 1
            outputArray[countsArray[countsArrayIndex] - 1] = arr[k]
            countsArray[countsArrayIndex]-- //Two equal input array elements should be placed in adjacent but different cells
            k--
        }
        return outputArray
    }

    override fun getName(): String {
        return "CountingSort"
    }
}
```
