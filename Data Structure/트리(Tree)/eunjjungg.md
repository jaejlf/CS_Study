
# 1. Tree

> 비선형 자료구조 : 데이터들의 관계들이 계층적으로 연관된 1:n or n:m 관계를 갖는 자료구조 <br/>
> → 하나의 데이터 뒤에 여러개의 데이터가 존재<br/>
node 개수가 n, edge의 개수는 n - 1
> 


![image](https://user-images.githubusercontent.com/100047095/182013587-49491c60-303c-46de-9ccd-11d9d141803d.png)

출처: [https://tutorialspoint.com](https://tutorialspoint.com/)<br/><br/>

1. Root : 최상단의 노드, Parent가 존재하지 않음 
2. Edge(간선) : Parent로부터 Child에게 이어지는 연결 선
3. Leaf : Child가 존재하지 않는 노드 
4. Level : 루트 노드로부터 level 0, depth에 따라 레벨이 늘어난다 
5. Siblings : 같은 부모를 가진 노드들의 집합
6. Descendant : 해당 노드로부터의 Child 노드들의 집합
7. Sub-tree : Child 노드의 Tree, 트리 안에 존재하는 트리를 의미
8. Node size : 자기 자신을 포함하여 그 노드가 가진 자손의 수 
9. Skew tree : 경사 트리. 모든 노드가 오직 한 개의 자손만을 가질 때 의미
    

![image](https://user-images.githubusercontent.com/100047095/182013593-f634d6a0-a1d3-40e5-aebe-65b0169f4cf2.png)

출처 : [https://genius-dev.tistory.com/entry/Kotlin자료구조-Tree에-대하여-1](https://genius-dev.tistory.com/entry/Kotlin%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Tree%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC-1)
<br/><br/>

# 2. Binary Tree

> 각 노드가 자식이 없거나, 최대 두 개의 노드로 구성된 트리
> 
<br/>
최종적인 자료 구조 모양에 따른 이름들이 존재

1. **Strict Binary Tree**
    
    모든 노드가 두 개의 자식을 가지거나 자식이 없는 트리<br/><br/>
    
2. **Full Binary Tree**
    
    모든 노드가 두 개의 자식을 가지고, leaf 노드가 같은 레벨에 있는 트리 
    
    모든 레벨에 노드들이 가득 채워진 형태 ! Full !
    
    | Level | Node Size |
    | --- | --- |
    | 0 | 2^0 |
    | 1 | 2^1 |
    | 2 | 2^2 |
    | … |  |
    | h | 2^h |
    | total | 2^(h+1) - 1 |
    
    `FBT`의 노드 개수는 2^(h+1) - 1
    
    높이가 h인 `CBT`의 노드 개수는 Level h - 1 인 FBT와 Level h 인 FBT의 노드의 총 개수 사이에 존재한다. 
    <br/><br/>
    
3. **Complete Binary Tree**
    
    마지막 레벨은 제외한 모든 레벨에서 노드들이 채워지고 마지막 레벨에서는 순차적으로 채워져 있는 트리
    
    루트부터 시작하여 각 노드에 순차적으로 번호를 매기면 트리 안의 노드 수까지 완전한 순열을 이룬다
    
    이진 트리의 높이가 `h`일 때 모든 리프 노드의 높이가 `h, h-1`이고 순열에서 빠진 숫자가 없을 때 CBT <br/><br/>
    


![image](https://user-images.githubusercontent.com/100047095/182013604-7036f2bb-193f-4807-8d0e-74bd0ee1f272.png)

출처 : [https://genius-dev.tistory.com/entry/Kotlin자료구조-Tree에-대하여-1](https://genius-dev.tistory.com/entry/Kotlin%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Tree%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC-1)
<br/>

```kotlin
//Kotlin code
class Node(
    var key: Int,
    var left: Node? = null,
    var right: Node? = null) 

//find
fun find(value: Int): Node? = when {
    this.value > value -> left?.findByValue(value)
    this.value < value -> right?.findByValue(value)
    else -> this
}

//insert 
fun insert(value: Int) {
    if (value > this.key) {
        if (this.right == null) {
            this.right = Node(value)
        } else {
            this.right.insert(value)
        }
    } else if (value < this.key) {
        if (this.left == null) {
            this.left = Node(value)
        } else {
            this.left.insert(value)
        }
    }
}

//removal
fun delete(value: Int) {
    when {
        value > key -> scan(value, this.right, this)
        value < key -> scan(value, this.left, this)
        else -> removeNode(this, null)
    }
}

//pre-order traversal
fun visit(): Array<Int> {
    val a = left?.visit() ?: emptyArray()
    val b = right?.visit() ?: emptyArray()
    return a + arrayOf(key) + b
}
```
<br/><br/>

# 3. Binary Tree의 탐색

> Binary Tree의 루트부터 시작하여 모든 노드를 탐색하는 데에는 세 가지 단계가 있음 <br/>
> 어떤 노드 순서로 방문할 건지에 따라 이름이 달라짐.
> 

![image](https://user-images.githubusercontent.com/100047095/182013611-3b119506-168d-48ef-9658-4977f4d2d1c5.png)

출처 : [https://genius-dev.tistory.com/entry/Kotlin자료구조-Tree에-대하여-1](https://genius-dev.tistory.com/entry/Kotlin%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Tree%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC-1)

<br/>

1. Pre-order traversal : 전위 탐색
    
    루트를 먼저 방문 → 왼쪽 서브 트리를 방문 → 오른쪽 서브 트리를 방문
    
    모든 탐색은 서브 트리로 진입했을 때도 같은 규칙을 적용함
    
    사진의 트리에 대해 1 - 2 - 4 - 5 - 3 순서로 탐색을 진행함 <br/><br/>
    
2. In-order traversal : 중위 탐색
    
    왼쪽 서브 트리를 먼저 방문 → 루트를 방문 → 오른쪽 서브 트리를 방문
    
    사진의 트리에 대해 4 - 2 - 5 - 1 - 3 순서로 탐색을 진행함<br/><br/>
    
3. Post-order traversal : 후위 탐색
    
    왼쪽 서브 트리를 먼저 방문 → 오른쪽 서브 트리를 방문 → 마지막으로 루트 노드를 방문 
    
    사진의 트리에 대해 4 - 5 - 2 - 3 - 1 순서로 탐색을 진행함 <br/><br/>
    

4. Level-order traversal
    
    트리의 레벨대로 순회하여 탐색함 
    
    사진의 트리에 대해 1 - 2 - 3 - 4 - 5 순서로 탐색을 진행함 
    <br/><br/>

# 4. Binary Search Tree

> 탐색 시 용이하게 만들기 위해 왼쪽 서브 트리에는 해당 노드보다 작은 값, 오른쪽 서브 트리에는 해당 노드보다 큰 값을 둠<br/>
시간 복잡도를 O(log n)으로 줄일 수 있음<br/>
그러나 최악의 경우 (ex. Skew tree) 는 여전히 O(n)으로 Binary Tree와 동일<br/>
> 
<br/>

**BST 구조**

1. 노드의 왼쪽 서브 트리는 모두 노드의 키 값보다 작은 키 값을 갖는 노드들로만 구성
2. 노드의 오른쪽 서브 트리는 모두 노드의 키 값보다 큰 키 값을 갖는 노드들로만 구성
3. 왼쪽과 오른쪽 서브 트리 모두 BST 
<br/>

**BST 특징**

1. 루트 데이터의 크기가 항상 왼쪽 서브 트리 데이터와 오른쪽 서브 트리 데이터 사이에 있기 때문에 중위 탐색을 수행하면 정렬된 리스트가 만들어진다 (중위 : 왼쪽 서브 트리 → 루트 → 오른쪽 서브 트리)
2. X를 검색할 때 왼쪽 서브 트리의 데이터가 X보다 작으면 왼쪽 서브 트리 검색은 생략한다. 
3. X를 검색할 때 오른쪽 서브 트리의 데이터가 X보다 크면 오른쪽 서브 트리 검색은 생략한다.
4. 이와 같이 생략 덕분에 시간 복잡도를 O(log n)으로 줄일 수 있음
<br/>

```kotlin
data class BinarySearchTreeNode(
        var data:Int,
        var left: BinarySearchTreeNode? = null,
        var right: BinarySearchTreeNode? = null
){

    fun insert(value:Int){
        if(value <= data && left != null){
            left!!.insert(value)
        }else if (value <= data){
            left = BinarySearchTreeNode(value)
        }else if(value> data && right != null){
            right!!.insert(value)
        }else{
            right = BinarySearchTreeNode(value)
        }
    }

    fun contains(value:Int) : Boolean{
        if (value < data && left !=null) {
            return left!!.contains(value)
        }
        if(value > data && right!=null) {
            return right!!.contains(value)
        }
        return value==data
    }

    fun search(value:Int) : BinarySearchTreeNode?{
        if (value < data && left !=null) {
            return left!!.search(value)
        }
        if(value > data && right!=null) {
            return right!!.search(value)
        }
        if (value==data) {
            return this
        }else{
            return null
        }
    }

    fun remove(value:Int) : Boolean {
        return remove(value, null)
    }

    fun remove(value:Int, parent:BinarySearchTreeNode?) : Boolean{
        if (value<data && left!=null){
            return left!!.remove(value,this)
        }else if(value<data){
            return false
        }else if(value>data && right != null){
            return right!!.remove(value,this)
        }else if (value>data){
            return false
        }else {
            if (left == null && right==null && this == parent?.left) {
                parent.left = null
            }else if (left == null && right==null && this==parent?.right){
                parent.right = null
            }else if(left!=null && right==null && this == parent?.left){
                parent.left = this.left
            }else if(left!=null && right== null && this == parent?.right){
                parent.right = this.left
            }else if (right!=null && left==null && this == parent?.left) {
                parent.left = this.right
            }else if(right!=null && left==null && this == parent?.right) {
                parent.right = this.right
            }else{
                data = right!!.min()
                right!!.remove(data,this)
            }
            return true
        }
    }

    fun min() : Int = if (left==null) data else left!!.min()
}

//출처 : https://github.com/JaimeDeArcos/kotlin-algorithms/blob/main/trees/src/main/kotlin/es/jaimedearcos/algorithms/tree/data/BinarySearchTreeNode.kt
```
