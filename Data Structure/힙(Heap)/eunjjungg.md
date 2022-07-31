# 1. Priority Queue

> FIFO 방식의 일반 Queue와 달리 우선순위가 큰 데이터가 먼저 나오는 큐
> 

**구현 방식**

1. Array : 데이터 삽입 시 들어갈 자리를 찾기 위해 O(n), 자리에 삽입된 후 각 데이터들을 shift하는데 O(n)의 시간 복잡도를 가짐
2. Linked List : 데이터 삽입 시 들어갈 자리를 찾기 위해 O(n)의 시간 복잡도를 가짐
3. Heap : 가장 좋은 방식, 데이터 삽입(offer()), 데이터 최댓값 최솟값 찾기(poll(), peek()), 데이터 검색(contains()) 시 O(log n)의 시간 복잡도를 가짐
<br/><br/>

# 2. Heap

> Heap은 최댓값, 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 Complete Binary Tree<br/>
주로 Binary Heap을 Heap이라고 부름!<br/>
**배열**로 구현함
> 
<br/>

**종류**

1. Max Heap, 최대 힙 : 부모 노드의 값이 자식 노드의 값보다 **크거나** 같음
2. Min Heap, 최소 힙 : 부모 노드의 값이 자식 노드의 값보다 **작거나** 같음

<br/>

**특징**
1. Max, Min Heap 둘 다 형제 관계에 있는 노드들 사이에는 **대소 규칙이 없음**
2. Max, Min Heap 둘 다 Tree의 왼쪽부터 채워짐

<br/><br/>

# 3. Heap 배열로 구현

![image](https://user-images.githubusercontent.com/100047095/182015628-01066856-7035-434b-8121-4b61937567f6.png)

출처 : [https://medium.com/depayse/kotlin-data-structure-collections-5-priorityqueue-184fc32e1ed9](https://medium.com/depayse/kotlin-data-structure-collections-5-priorityqueue-184fc32e1ed9)

<br/>

계산을 용이하게 하기 위해 0번째 index는 사용하지 않음

Root 노드의 index를 1로 하고 형제 노드끼리는 왼쪽부터 오른쪽 방향으로 index를 부여함

그러면 규칙이 생성 됨

```kotlin
1. 왼쪽 자식 노드의 index = 부모 노드의 index * 2
2. 오른쪽 자식 노드의 index = 부모 노드의 index * 2 + 1
3. 부모 노드의 index = 자식 노드의 index / 2
```
<br/><br/>

# 4. Heap : 데이터 삽입 & 삭제

![image](https://user-images.githubusercontent.com/100047095/182015616-8c28e3c9-5528-40c7-935a-8709efaa54b8.png)

출처 : [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

<br/>

**삽입**

1. Complete Binary Tree의 규칙에 맞도록 마지막 노드에 새로운 데이터 삽입
2. 부모 노드와 비교하면서 Max Heap의 경우 부모 노드의 값보다 클 때, Min Heap의 경우 부모 노드의 값보다 작을 때 부모 노드와 교체
<br/><br/>

![image](https://user-images.githubusercontent.com/100047095/182015606-1f2fcc5c-8c59-48e7-b263-d2ab138fefd6.png)

출처 : [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

<br/>

**삭제**

1. Max Heap의경우 가장 큰 데이터인 Root Node가, Min Heap의 경우 가장 작은 데이터인 Root Node가 삭제됨
2. CBT인 Heap의 가장 마지막 Node를 Root 자리에 올림
3. 자식 노드와 비교하며 Max Heap의 경우 자식 노드의 값보다 작을 때, Min Heap의 경우 자식 노드의 값보다 클 때 자식 노드와 교체 (재배열)
<br/><br/><br/>


# 5. PriorityQueue in Kotlin

> Kotlin의 PriorityQueue는 값이 작을 수록 우선 순위가 높은 것으로 여김<br/>
Kotlin의 PriorityQueue는 Heap으로 구현됨
> 

<br/>

**메소드**

```kotlin
offer(e E) : Priority Queue에 객체를 추가, 추가 됐으면 true, 아니면 false return

poll : Priority Queue에 순서상 가장 먼저 들어간 객체를 제거하고 반환
-> Priority Queue가 빈 상태였다면 null return 

peek : Priority Queue의 가장 앞쪽에 있는 객체를 찾아서 반환
-> Priority Queue가 빈 상태였다면 null return 

clear : Priority Queue의 모든 데이터 삭제

comparator : Priority Queue를 정렬하는데 사용된 comparator를 반환
-> natural order일 땐 null return 
```

<br/>

**사용 방법**

```kotlin
//Kotlin code 
fun main() {
    //초기 용량이 11이고 natural order로 정렬되는(Min Heap) Priority Queue 생성
    val pq= PriorityQueue<Int>()
    //초기 용량 설정
    val pq2= PriorityQueue<Int>(50)
    //MaxHeap 구성(초기 용량 11): 람다 식으로 comparator 전달
    val pq3= PriorityQueue<Int> {o1,o2 -> o2.compareTo(o1)}
    //초기 용량 설정된 MinHeap 구성: 람다 식으로 comparator 전달
    val pq4= PriorityQueue<Int>(50) {o1,o2 -> o2.compareTo(o1)}
}
```

```kotlin
//Kotlin code 
fun main() {
    //초기 용량이 11이고 reverse order : Max Heap pq 생성
    val pq = PriorityQueue<Int>(reverseOrder())
    println("처음 pq: $pq")

    //priority queue에 offer하기
    pq.offer(25)
    pq.offer(20)
    pq.offer(18)
    pq.offer(13)
    pq.offer(17)
    pq.offer(16)
    pq.offer(11)
    pq.offer(5)

    //priority queue 출력 : Heap의 배열이 순서대로 출력됨
    println("데이터 삽입 후 pq: $pq")

    //priority queue에서 최댓값을 뽑고 삭제
    println("pq.poll() : ${pq.poll()}")
    //최댓값 삭제 후 출력
    println("최댓값 삭제 후 pq: $pq")

    //현재 priority queue의 최댓값 보기
    println("pq.peek() : ${pq.peek()}")
    println("peek 이후 pq $pq")
}

/* 결과 :
처음 pq: []
데이터 삽입 후 pq: [25, 20, 18, 13, 17, 16, 11, 5]
pq.poll() : 25
최댓값 삭제 후 pq: [20, 17, 18, 13, 5, 16, 11]
pq.peek() : 20
peek 이후 pq [20, 17, 18, 13, 5, 16, 11]
*/
```
