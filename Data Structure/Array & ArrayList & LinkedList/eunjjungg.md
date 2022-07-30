# 1. Array

> 같은 자료형을 가진 값들을 하나로 나타낸 것<br/>
초기화와 동시에 크기가 정해짐<br/>
메모리 공간에 `연속적`으로 저장됨<br/>
Index로 값에 접근<br/>
**정적** 타입
> 

### 장점

1. 인덱스를 통한 검색이 용이함!
2. 연속된 메모리를 사용하므로 메모리 관리가 편리함

### 단점

1. 배열에서 값을 삭제할 경우 빈 공간 그대로 남아있어 메모리가 낭비됨
2. 배열은 정적이므로 배열의 크기를 컴파일 이전에 지정해야 됨
3. 배열의 크기를 한 번 정하고 나면 재조정할 수 없음. 
<br/>

# 2. List

> Kotlin에 존재하는 Read-Only List Collection<br/>
데이터가 변경될 일이 없을 시에는 List 사용을 권장 <br/>
(변경 될 일이 있다면 MutableList 사용을 권장)
> 
<br/>

# 3. Mutable List

> List를 상속하여 만들어짐<br/>
추가, 삭제 등 수정이 가능한 리스트<br/>
말 그대로 Mutable한 List임
> 
<br/>

# 4. Array List

> 내부가 Array로 구현되어 있는 추가, 삭제 등 수정이 가능한 리스트<br/>
MutableList 중에서도 Array List를 사용하겠다는 의미
> 

원하는 데이터를 index를 통해 직접 접근하므로 `O(1)`의 복잡도를 가짐<br/>
데이터를 추가, 삭제할 경우 뒤의 데이터 블록들을 하나씩 shift하므로 `O(n)`의 복잡도를 가짐<br/>

연속된 메모리 공간을 사용함<br/>
Array와 다르게 길이가 동적으로 할당될 수 있음 <br/>
Linked List와 다르게 공간을 한 번 할당하면 추가할 때 마다 특별하게 들어가는 자원이 없음 <br/>

`Android의 RecyclerView Adapter`의 경우 ArrayList로 List를 사용하는 것이 효율적임! <br/>
왜냐하면 보통 해당 원소의 Position을 알고 그 위치를 참조하므로 참조시 O(1)의 복잡도를 가진 ArrayList가 이득<br/>

```kotlin
//code in Kotlin
fun main() {
    val arr = ArrayList<Int>(5) //초기 크기를 설정
    val arr2 = arrayListOf<Int>(10,11,12)   //arrayList에 들어갈 객체 나열
    val arr3 = ArrayList(arr2)  //Collection(arr2)을 인자로 받아 arrayList 생성

		//ex
		val arrayList: ArrayList<String> = ArrayList()
    arrayList.add("1")
    arrayList.addAll(arrayOf("2", "3"))
    arrayList.add(0, "Head")
    arrayList.add(arrayList.size, "Tail")
    //result : [Head, 1, 2, 3, Tail]
}
```
<br/>

# 5. Linked List

> 데이터를 저장하는 data와 다른 노드와의 연결 고리인 link로 구성되어 있는 Node로 구성된 리스트
> 

Array List에 비하여 메모리 공간 효율이 떨어짐<br/>
반면 데이터의 추가나 삭제는 Array List보다 효율이 좋음 <br/>
원하는 데이터를 찾아가려면 해당 노드까지 링크를 통해 찾아야하므로 `O(n)`의 복잡도를 가짐 <br/>
메모리에 연속적으로 할당되어 있지 않아 공간 최적화의 이점 X<br/>

```kotlin
//code in Kotlin
fun main() {
    val linkedList1 = LinkedList<Char>() //빈 LinkedList생성
    val linkedList2 = LinkedList(linkedList1)    //Collection을 인자로 받아 linkedList 생성
		
		//ex
		val linkedList: LinkedList<String> = LinkedList()
		linkedList.addAll(arrayOf("2", "3"))
		linkedList.addFirst("Head")
		linkedList.addLast("Tail")
		//result : [Head, 2, 3, Tail]
}
```
