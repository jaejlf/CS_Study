# 💡 Stack

- 한 쪽 끝에서만 접근할 수 있는 선형 자료구조.
- `LIFO` (Last In First Out, 후입선출): 가장 늦게 들어온 것이 가장 먼저 나온다.

</br>

![Data_stack](https://user-images.githubusercontent.com/75151848/181554374-4f9ca467-81dd-4690-b42d-5627aa7a8ff6.svg)

</br>

## 사용 사례

- 함수의 콜스택
- 재귀 알고리즘, DFS 알고리즘
- 후위표기법
- 문자열 역순 출력
- 괄호 검사

</br>

## 연산

- pop(): 스택에서 가장 위에 있는 항목을 제거한다.
- push(item): item 하나를 스택의 가장 윗 부분에 추가한다.
- peek(): 스택의 가장 위에 있는 항목을 반환한다.
- isEmpty(): 스택이 비어 있을 때에 true를 반환한다.

</br>

## 사용 예제 (Java)

- Stack은 내부적으로 `Vector` 를 상속한다.

```java
Stack<E> stack = new Stack<>();

stack.push(item);     // 아이템 추가
stack.pop();          // 아이템 제거
stack.peek();         // 가장 위쪽 아이템 출력
stack.empty();        // 스택이 비어있는지 check
stack.clear();        // 전체 아이템 제거
stack.contains(item); // 아이템이 있는지 check
```

</br></br>

# 💡 Queue

- 입력과 출력을 한 쪽 끝(`front`, `rear`)으로 제한하는 자료구조.
    - `front`: 첫 번째 요소를 가리킨다. 데이터가 제거되는 곳.
    - `rear`: 마지막 원소를 가리킨다. 데이터가 삽입되는 곳.
- `FIFO` (First In First Out, 선입선출) : 가장 먼저 들어온 것이 가장 먼저 나온다.

</br>

![Data_Queue](https://user-images.githubusercontent.com/75151848/181563975-cbb04ad9-2b1c-489b-b563-608f98a64121.svg)

</br>

## 사용 사례

- BFS 알고리즘
- 컴퓨터 버퍼. 마구 입력이 되었으나 처리를 하지 못할 때, 버퍼(큐)를 만들어 대기 시킨다.
- 캐시(Cache) 구현
- 우선순위가 같은 작업 예약 (인쇄 대기열)
- 선입선출이 필요한 대기열 (티켓 카운터)
- 프린터의 출력 처리

</br>

## 연산

- enqueue: 데이터를 맨 뒤에 삽입한다.
- dequeue: 맨 앞에 있는 데이터를 제거한다.

</br>

## 사용 예제 (Java)

### 1. Linear Queue

- 선형 큐
- Java에서는, 끝에 요소를 추가하기 용이한 `LinkedList`를 통해 `Queue` 인터페이스를 구현할 수 있다.

```java
Queue<E> queue = new LinkedList<>();

// 아이템 추가
queue.add(item);        // 가득찬 경우 예외 발생
queue.offer(item);      // 가득찬 경우 false 반환

// 첫 번째 아이템 반환 및 삭제
queue.remove();         // 비어있는 경우 예외 발생
queue.poll();           // 비어있는 경우 null 반환

// 첫 번째 아이템 반환
queue.element();        // 비어있는 경우 예외 발생
queue.peek();           // 비어있는 경우 null 반환

// 전체 아이템 제거
queue.clear();
```

</br>

### 2. Circular Queue

- 원형 큐, 순환 큐
- 논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주하는 큐.
- 선형 큐의 경우, rear가 끝에 도달했을 때 큐에 빈 공간이 있어도 가득 찬 것으로 판단하기 때문에 메모리가 낭비될 수 있다.
- 이를 해결하기 위한 것이 circular queue이다.

```java
public CircualrQueue {
	private int size = 0; 
	private int rear = 0; 
	private int front = 0;
	private Object[] queue;
	
	CircualrQueue(int size) { 
	    this.size = size;
	    this.queue = new Object[size];
	}
	
	public void enQueue(Object o) {
	    if(isFull()) {
	        return;
	    }
	    rear = (++rear) % size;
	    queue[rear] = o;
	}
	
	
	public Object deQueue(Object o) {
	    if(isEmpty()) { 
	        return null;
	    }
	    
	    front = (++front) % size;
	    Object o = queue[front];
	    return o;
	}
	
	public Object deQueue(Object o) {
	    if(isEmpty()) { 
	        return null;
	    }
	    front = (++front) % size;
	    Object o = queue[front];
	    return o;
	}
	
	public boolean isEmpty() {
	    return front == rear;
	}
	
	public boolean isFull() {
	    return (rear == queueSize-1);
	}
}
```

</br>

### 3. Priority Queue

- 우선순위 큐
- 우선순위가 높은 데이터가 먼저 나가는 자료구조.
- 내부 요소는 이진트리 구조로써, `Heap`으로 구성되어 있다.

```java
PriorityQueue<E> priorityQueue = new PriorityQueue<>();

//낮은 숫자가 우선 순위인 int 형 우선순위 큐 선언
PriorityQueue<Integer> priorityQueueLowest = new PriorityQueue<>();

//높은 숫자가 우선 순위인 int 형 우선순위 큐 선언
PriorityQueue<Integer> priorityQueueHighest = new PriorityQueue<>(Collections.reverseOrder());

// 아이템 추가
priorityQueue.add(item);
priorityQueue.offer(item);  

// 우선순위가 가장 높은 아이템 반환 및 삭제
priorityQueue.remove();    
riorityQueue.poll();

// 우선순위가 가장 높은 아이템 반환
priorityQueue.element();
priorityQueue.peek();

// 전체 아이템 삭제
priorityQueue.clear();
```

</br></br>

# 💡 Deque(덱, 데크)

- **Double - Ended Queue**의 줄임말
- 양쪽 끝(`head`, `tail`)에서 데이터 삽입 및 삭제가 가능한 자료구조.

![deque](https://user-images.githubusercontent.com/75151848/181554586-d3b60e6d-9eed-42a1-a08c-78f9caccbd50.png)

</br>

## 사용 사례

- 데이터를 앞, 뒤쪽에서 모두 삽입 삭제하는 과정이 필요한 경우

</br>

## 사용 예제 (Java)

```java
Deque<E> deque = new ArrayDeque<Integer>();

// 아이템 추가
deque.offerFirst(item);   // 앞으로 삽입
deque.offerLast(item);    // 뒤로 삽입

deque.addFirst(item);     // 앞으로 삽입
deque.addLast(item);      // 뒤로 삽입

// 아이템 반환 및 삭제
deque.pollFirst();        // 앞에꺼 추출
deque.pollLast();         // 뒤에꺼 추출

deque.removeFirst();      // 앞에꺼 추출
deque.removeLast();       // 뒤에꺼 추출

// 아이템 반환
deque.peekFirst();        // 앞에꺼 반환
deque.peekLast();         // 뒤에꺼 반환

deque.getFirst();         // 앞에꺼 반환
deque.getLast();          // 뒤에꺼 반환
```

- 이외에도, Stack과 Queue의 메소드들(push, pop, …)도 사용 가능하다.

</br></br>

# ⏳ Time Complexity

|  | 삽입 | 삭제 |
| --- | --- | --- |
| Stack (후입선출) | O(1) | O(1) |
| Queue (선입선출) | O(1) | O(1) |
| Prioriy Queue (힙) | 𝑂(𝑙𝑜𝑔𝑁) | 𝑂(𝑙𝑜𝑔𝑁) |
| Deque | O(1) | O(1) |

</br></br>
