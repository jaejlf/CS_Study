## 💡 Array

- 메모리 공간에 할당할 크기를 미리 정해놓는 자료구조.
- 크기를 동적으로 변경할 수 없다.
- 데이터가 계속해서 늘어날 때나 최대 사이즈를 알 수 없는 경우에 부적합하다.
- 데이터를 중간에 삽입하거나 삭제할 때 비효율적이다.
- index로 빠르게 값을 찾을 수 있다.

</br></br>

## 💡 ArrayList

- 크기가 정해져 있지 않은 자료구조로, 내부적으로 배열의 형태를 가진다.
즉, 요소들이 메모리에 연속적으로 존재한다.
- 크기를 변경할 수 있다.
- 순서가 중요하며, index를 가지고 있어 검색이 빠르다.
- 데이터를 중간에 삽입하거나 삭제할 때, 요소들을 한 칸씩 뒤로 미루거나 앞으로 당기는 연산을 하기 때문에 오래 걸린다.

</br>

![arraylist](https://user-images.githubusercontent.com/75151848/181026835-af019d05-0d33-4d8c-881c-50086c70fe26.png)  

</br>

### 사용 예제
```java
List<E> list = new ArrayList<>();

list.get(index);            // 인덱스에 해당하는 원소 조회
list.set(index, element);   // 인덱스에 해당하는 원소 설정
list.add(element);          // 맨뒤에 원소 추가
list.add(index, element);   // 지정 인덱스에 원소 추가
list.remove(index);         // 인덱스에 해당하는 원소 삭제
```
</br></br>

## 💡 LinkedList

- 한 노드에 연결될 노드의 포인터 위치를 가리키는 방식으로 구성된다.
    - 단일 연결리스트: 뒷 노드만 가리킨다.
    - 다중 연결리스트: 앞뒤 노드를 모두 가리킨다.
- 데이터를 삽입하거나 삭제할 때 빠르다.
- index가 없어 임의의 데이터에 접근 시 순차 탐색을 하기 때문에 검색이 느리다.


![linkedlist](https://user-images.githubusercontent.com/75151848/181027860-df83e644-e7b6-4253-bee0-95f792dde3d2.png)  

### 사용 예제
```java
List<E> list = new LinkedList<>();

list.get(index);            // 인덱스에 해당하는 원소 조회
list.set(index, element);   // 인덱스에 해당하는 원소 설정
list.add(element);          // 맨뒤에 원소 추가
list.add(index, element);   // 지정 인덱스에 원소 추가
list.remove(index);         // 인덱스에 해당하는 원소 삭제
```
</br></br>


## ⏳ Time Complexity
|  | ArrayList | LinkedList |
| --- | :---: | :---: |
| get / set | O(1) | O(n) |
| add(시작) | O(n) | O(1) |
| add(끝) | O(1) | O(1) |
| add(중간) | O(n) | O(n) |
| remove(시작) | O(n) | O(1) |
| remove(끝) | O(1) | O(1) |
| remove(중간) | O(n) | O(n) |

</br></br>


## 📌 정리

get/set을 자주 사용한다면? **ArrayList**

처음이나 끝에 잦은 삽입, 삭제가 발생한다면? **LinkedList**

</br></br></br> 
