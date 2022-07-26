
## 📍 Stack, 스택
![image](https://user-images.githubusercontent.com/78673570/181016352-c508972c-a738-4e8e-b634-3cefba4923e4.png)

-   입력과 출력이 한 곳(방향)으로 제한
-   스택 = 쌓아 올리는, 즉 차곡차곡 쌓아 올린 형태의 자료 구조
-   LIFO ( Last In First Out) : 가장 나중에 들어온 것이 가장 먼저 나온다.
-   stack underflow  
    \= 비어있는 스택에서 원소를 추출하려고 할 때
-   stack overflow  
    \= 스택이 넘치는 경우

<br>

### 사용법

```java
Stack<Integer> stack = new Stack<>();  // 스택 선언
stack.push(1);                         // 값 추가
stack.pop();                           // 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
stack.clear();                         // 전체 값 제거 (스택 초기화)
stack.peek();                          // 가장 상단의 값 출력
stack.size();                          // 스택의 크기 출력
stack.empty();                         // 스택이 비어있는지 체크 -> T/F 반환
stack.contains(1);                     // 스택에 특정 요소가 있는지 체크 -> T/F 반환
```

<br>

### 스택 활용 예시

-   웹 브라우저 방문 기록 (= 뒤로가기) : 가장 나중에 열린 페이지부터 다시 보여준다.
-   역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력
-   실행 취소 : 가장 나중에 실행된 것부터 실행 취소

<br><br>

## 📍 Queue, 큐
![image](https://user-images.githubusercontent.com/78673570/181016478-1fdd5c57-8529-45b7-b5d1-01aa5a207279.png)

-   한 쪽(뒤쪽, rear)에선 삽입, 다른 한 쪽(앞쪽, front)에선 삭제 → 양쪽에서 작업이 이루어진다.
-   큐 = 줄을 서서 기다리는, 즉 먼저 온 것을 먼저 처리하는 형태의 자료 구조
-   FIFO ( First In First Out) : 먼저 들어온 것이 먼저 나온다.

<br>

### 사용법

```java
Queue<Integer> queue= new LinkedList<>();  // 큐 선언
queue.add(1);                              // 값 추가 -> 성공 시 T, 실패 시 예외 발생
queue.offer(2);                            // 값 추가 -> 성공 시 T, 실패 시 F 발생
queue.clear();                             // 전체 값 제거 (큐 초기화)
queue.remove();                            // 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
queue.poll();                              // 값 제거 -> 리턴 후 제거, 비어있다면 null 리턴
queue.element();                           // 첫 번째 값 리턴 -> 비어있다면 예외 발생
queue.peek();                              // 첫 번째 값 리턴 -> 비어있다면 null 리턴
queue.size();                              // 큐의 크기 출력
queue.isEmpty();                           // 큐가 비어있는지 체크 -> T/F 반환
queue.contains(1);                         // 큐에 특정 요소가 있는지 체크 -> T/F 반환
```

<br>

### 큐 활용 예시

- 우선순위가 같은 작업의 예약 (ex. 프린터의 인쇄 대기열)
- 은행 업무
- 콜센터 고객 대기 시간
- 캐시(Cache 구현)

<br><br>

## 📍 Priority Queue, 우선순위 큐

-   일반적인 큐와 다르게, 우선순위를 먼저 결정하고 그 우선순위가 높은 것이 먼저 나가는 형태의 자료 구조
-   힙(Heap)을 통해 구현하는 것이 일반적 ⇒ 우선순위를 기준으로 최대힙 혹은 최소힙을 구성

<br>

### 사용법

```java
PriorityQueue<Integer> pq = new PriorityQueue<>(); // 우선순위가 낮은 것 - 오름차순
PriorityQueue<Integer> pq_rev = new PriorityQueue<>(Collections.reverseOrder()); // 우선순위가 높은 것 - 내림차순
pq.add(1);                              // 값 추가 -> 성공 시 T, 실패 시 예외 발생
pq.offer(2);                            // 값 추가 -> 성공 시 T, 실패 시 F 발생
pq.remove();                            // 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
pq.poll();                              // 값 제거 -> 리턴 후 제거, 비어있다면 null 리턴
pq.clear();                             // 전체 값 제거 (큐 초기화)
pq.element();                           // 첫 번째 값 리턴 -> 비어있다면 예외 발생
pq.peek();                              // 첫 번째 값 리턴 -> 비어있다면 null 리턴
pq.size();                              // 큐의 크기 출력
pq.isEmpty();                           // 큐가 비어있는지 체크 -> T/F 반환
pq.contains(1);                         // 큐에 특정 요소가 있는지 체크 -> T/F 반환
```

<br>

### 우선순위큐 활용 예시

-   우선순위가 중요한 상황 (ex. 응급실)

<br><br>

## 📍 Dequeue, 덱
![image](https://user-images.githubusercontent.com/78673570/181016888-ae0007de-44d3-481c-8529-725154446f1e.png)

-   Double Ended Queue = 양쪽에서 삽입과 삭제를 수행할 수 있는 형태의 자료 구조

<br>

### 사용법

```java
Deque<Integer> dq = new LinkedList<>(); // 큐 선언
dq.add(1);                              // 맨 앞에 값 추가 -> 성공 시 T, 실패 시 예외 발생
dq.addFirst(0);                         // 맨 앞에 값 추가 -> 성공 시 T, 실패 시 예외 발생
dq.addLast(100);                        // 맨 뒤에 값 추가 -> 성공 시 T, 실패 시 예외 발생
dq.offer(2);                            // 맨 앞에 값 추가 -> 성공 시 T, 실패 시 F 발생
dq.offerFirst(2);                       // 맨 앞에 값 추가 -> 성공 시 T, 실패 시 F 발생
dq.offerLast(2);                        // 맨 뒤에 값 추가 -> 성공 시 T, 실패 시 F 발생
dq.remove();                            // 맨 앞에 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
dq.removeFirst();                       // 맨 앞에 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
dq.removeLast();                        // 맨 뒤에 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
dq.poll();                              // 맨 앞에 값 제거 -> 리턴 후 제거, 비어있다면 null 리턴
dq.pollFirst();                         // 맨 앞에 값 제거 -> 리턴 후 제거, 비어있다면 null 리턴
dq.pollLast();                          // 맨 뒤에 값 제거 -> 리턴 후 제거, 비어있다면 null 리턴
dq.getFirst();                          // 맨 앞의 값 리턴 -> 비어있다면 예외 발생
dq.getLast();                           // 맨 뒤의 값 리턴 -> 비어있다면 예외 발생
dq.peek();                              // 맨 앞의 값 리턴 -> 비어있다면 null 리턴
dq.peekFirst();                         // 맨 앞의 값 리턴 -> 비어있다면 null 리턴
dq.peekLast();                          // 맨 뒤의 값 리턴 -> 비어있다면 null 리턴
dq.removeFirstOccurrence(x);            // 맨 앞에서부터 탐색하여, x와 동일한 첫 원소 제거
dq.removeLastOccurrence(x);             // 맨 뒤에서부터 탐색하여, x와 동일한 첫 원소 제거
dq.element();                           // 첫 번째 값 리턴 -> 비어있다면 예외 발생
dq.push(2);                             // 맨 앞에 값 추가 -> 실패 시 예외 발생
dq.pop();                               // 맨 앞에 값 제거 -> 리턴 후 제거, 비어있다면 예외 발생
dq.remove(x);                           // removeFirstOccurrence와 동일
pq.size();                              // 덱의 크기 출력
pq.isEmpty();                           // 덱이 비어있는지 체크 -> T/F 반환
pq.contains(1);                         // 덱에 특정 요소가 있는지 체크 -> T/F 반환
```
