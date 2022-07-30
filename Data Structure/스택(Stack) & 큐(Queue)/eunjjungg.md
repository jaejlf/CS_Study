# 1. Stack

> : **쌓는다**! 
LIFO (Last In First Out, 후입선출) or FILO (First In Last Out, 선입후출)<br/>
→ 먼저 저장된 항목일 수록 나중에 사용할 수 있음<br/>
> 
<br/>
코틀린에서의 Stack은 단일 클래스로 존재<br/>
데이터를 넣는 것은 Push, 데이터를 꺼내는 것을 Pop이라고 함 <br/>
코틀린에서의 Push()와 Pop()은 이름 그대로 함수로 존재함 <br/>
<br/>

```kotlin
//Kotlin 메소드 목록
push(item: E) : Stack의 최상단에 item을 올림
pop : Stack의 최상단에 있는 객체를 제거하고 return함
peek : Stack의 최상단의 객체를 단순 return함
empty : Stack이 비었다면 true, 그렇지 않으면 false를 return 

search(object: O) : object가 Stack의 어느 위치에 있는지 찾는다.
-> Stack의 최상단에 있는 객체의 위치를 1로 하고,
하단으로 갈 수록 1씩 늘어가는 위치를 반환한다. 
찾는 객체가 없다면 -1를 return 
```
<br/>

```kotlin
//Kotlin code 
//1. Stack Class 사용 
val stack = Stack<Char>()
stack.push('A')
stack.pop()

//2. Linked List 클래스를 이용하여 Stack 사용하기 
val stackLL = LinkedList<Char>()
val stackLL2 = LinkedList<Char>(stackLL)//Collection을 인자로 받아 Stack 생성
stackLL.push('A')
stackLL.push('B')
stackLL.push('C')
stackLL.pop()

```
<br/>

![image](https://user-images.githubusercontent.com/100047095/181997271-f491c9a5-66d2-4364-ad9c-1cd734484ebb.png)

출처 : [https://medium.com/depayse/kotlin-data-structure-collections-4-stack-queue-deque-4c383efebee9](https://medium.com/depayse/kotlin-data-structure-collections-4-stack-queue-deque-4c383efebee9)
<br/><br/>

# 2. Queue

> : 줄, 대기 행렬
FIFO (First In First Out, 선입선출) or LILO (Last In Last Out, 후입후출)
> 
<br/>
데이터의 흐름은 한 쪽으로만 움직임<br/>
데이터를 추가하는 것을 Enqueue, 꺼내는 것을 Dequeue라고 하지만 Kotlin에서는 offer(), pull()의 함수로 존재
<br/>

```kotlin
//Kotlin 메소드 목록
add(e E) : Queue에 객체를 추가한다
offer(e E) : Queue에 객체를 추가하는데 객체가 성공적으로 추가되면 true, 아니면 false를 return 

remove : Queue의 순서상 가장 먼저 들어간 객체를 삭제하고 반환
-> 만약 Queue가 비어있다면 Exception을 throw함

element : Queue의 순서상 가장 먼저 들어간 객체를 찾아 반환
-> 만약 Queue가 비어있다면 Exception을 throw함

poll : Queue의 순서상 가장 먼저 들어간 객체를 삭제하고 반환
-> 만약 Queue가 비어있다면 null을 return 

peek : Queue의 순서상 가장 먼저 들어간 객체를 찾아 반환
-> 만약 Queue가 비어있다면 null을 return 
```
<br/>

```kotlin
//Kotlin Code
//1. LinkedList 클래스 이용하여 Queue 사용
val queueLL = LinkedList<Char>()
val queueLL2 = LinkedList<Char>(queueLL)
queueLL.offer('A')
queueLL.offer('B')
queueLL.offer('C')
//A, B, C

queueLL.poll()
//B, C

queueLL.peek()
//B, C
```
<br/>

![image](https://user-images.githubusercontent.com/100047095/181997282-eddc99de-f428-4602-af97-3a60b6e024d8.png)

출처 : [https://medium.com/depayse/kotlin-data-structure-collections-4-stack-queue-deque-4c383efebee9](https://medium.com/depayse/kotlin-data-structure-collections-4-stack-queue-deque-4c383efebee9)
