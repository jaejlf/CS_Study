# Stack & Queue

## A. 스택(Stack)이란?

<p align="center" style="color:gray">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Data_stack.svg/440px-Data_stack.svg.png" height=180>
</p>

- **한 쪽 끝**에서만 원소를 넣거나 뺄 수 있는 자료구조 → 특정 위치에서만 원소 넣거나 뺄 수 있으므로 Restricted Structure
- 가장 나중에 들어간 원소가 가장 먼저 나오게 되는 **LIFO(Last In First Out)** 구조
  <br/>ex) 원통형 과자 통, 카드 덱, 팬케이크
- 원소의 추가/제거 → `O(1)`
  - 원소가 추가되는 곳: top
- 가장 상단의 원소 확인 → `O(1)`
- 상단이 아닌 나머지 원소 확인/변경 **원칙적으로 불가능**
- 스택의 기본 연산
  - `push` : 스택의 끝에 원소 추가
  - `pop` : 스택의 끝 원소 제거

<br>

**_언제 사용?_**

함수의 콜스택, 문자열 역순 출력, 연산자 후위표기법, iOS의 네비게이션 스택, 트리와 그래프 검색 문제

<br>

## B. 큐(Queue)란?

<p align="center" style="color:gray">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/600px-Data_Queue.svg.png" height=180>
</p>

- 한 쪽 끝에서 원소를 넣고 반대쪽 끝에서 원소를 뺄 수 있는 자료구조
- 먼저 들어간 원소가 먼저 나오게 되는 **FIFO(First In First Out) 구조**
- Restricted Structure
- 원소의 추가/제거(enQueue/deQueue) → `O(1)`
  - 원소가 추가되는 곳: rear
  - 원소가 제거되는 곳: front
- 제일 앞/뒤 원소 확인 → `O(1)`
- 제일 앞/뒤가 아닌 나머지 원소 확인은 원칙적으로 불가능
- 큐의 종류
  - 선형 큐
  - 원형 큐
  - 우선순위 큐
    <br>
    <br/>

## C. Stack in Swift

(raywenderlich의 Data Structure & Algorithm in Swift를 참고하였습니다.)

```Swift
public struct Stack<Element> {

  private var storage: [Element] = []

  public init() { }
}
```

Stack을 배열로 구현했다. 배열의 `append/popLast`모두 배열의 한 쪽 끝에서 일어나기 때문이다.

따라서 스택의 `push`는 `append`로, `pop`은 `popLast`로 구현할 수 있다.

```Swift
  var stack = Stack<Int>()
  stack.push(1)
  stack.push(2)
  stack.push(3)
  stack.push(4)

  print(stack)  // 4(top) - 3 - 2 - 1
```

이렇게 구현한 스택의 `push`와 `pop` 모두 시간복잡도는 `O(1)`이다.
<br>
<br/>

## D. Queue in Swift

(raywenderlich의 Data Structure & Algorithm in Swift를 참고하였습니다.)
<br><br/>

```Swift
var queue = Queue<Int>()
queue.enqueue(10) // [ 10 ]
queue.enqueue(3)  // [ 10, 3 ]
queue.enqueue(57) // [ 10, 3, 57 ]
queue.dequeue()   // print(10), 남은 큐는 [ 3, 57 ]
```

Swift에서는 큐(Queue)를 기본 자료형으로 제공하지 않는다. 따라서 직접 구현해서 사용하여야 한다.

<br/>

```Swift
public protocol Queue {
  associatedtype Element
  mutating func enqueue(_ element: Element) -> Bool
  mutating func dequeue() -> Element?
  var isEmpty: Bool { get }
  var peek: Element? { get }
}
```

- `enqueue`: 큐의 맨 뒤에 원소를 추가한다. 원소 추가에 성공하였으면 true를 리턴한다.
- `dequeue`: 큐의 맨 앞 원소를 제거하고 제거한 원소를 리턴한다.
- `isEmpty`: 큐가 비었는지 체크한다.
- `peek`: 큐를 첫번째 원소를 제거하지 않고 리턴만 한다.

<br/>
큐의 삭제는 항상 맨 앞(front)에서 일어나고 큐의 추가는 항상 맨 뒤(rear)에서 일어난다는 점을 유의해야 한다.

<br>
Swift에서 큐를 구현할 수 있는 방법은 다양하다.

- Array로 구현
- Doubly Linked List로 구현
- Ring buffer로 구현
  - 크기가 고정된 큐에 효과적
- Double-stack으로 구현
  - 다른 구현 방법에 비해 `dequeue(_:)` 시간 복잡도를 O(1)로 개선할 수 있음
