# 📍 Array

- 배열
- 각각의 요소(element)에 인덱스(index)를 부여해서 해당하는 데이터를 불러오는 자료구조
- 메모리 공간에 할당할 사이즈를 미리 정해놓고 사용하는 자료구조
- 연속된 메모리 공간에 순차적으로 저장된 데이터 모음

<br>

## 특징

### 1. 선언할 때 크기와 데이터 타입을 지정해야한다.

```java
int[] arr = new int[5];
String[] arr = new String[5]; 
```
- 메모리 할당 시 길이를 늘릴 수 없다.  
따라서 데이터의 최대 사이즈를 알 수 없는 경우에는 사용하기 부적합하고, 사용하지 않는공간이라도 해당 메모리 공간을 차지하고 있기 때문에 메모리가 낭비될 수 있다.

- 요소의 삽입/삭제가 비효율적이다.  
요소를 중간에 삽입/삭제할 경우 항상 메모리가 순차적으로 이어져 있어야 하기 때문에, 해당 요소 뒤에 있는 모든 요소의 자리 이동이 필요하기 때문에 매우 비효율적이다. ( => 삽입/삭제가 빈번하게 발생하는 프로세스의 경우 치명적 ! )

- 동일한 자료형  
배열의 요소들은 모두 동일한 자료형을 가진다.

<br>

### 2. 빠른 검색 성능

'인덱스'를 사용하기 때문에 무작위 접근(random access)가 가능하여 검색이 편하다.

<br>

### 3. 데이터가 순차적으로 저장된다.

실제 메모리 상에서 데이터가 순차적으로 저장되기 때문에 데이터에 순서가 있으며, 인덱스가 존재하여 `indexing` 및 `slicing`이 가능하다.

- indexing : 인덱스를 사용해 특정 요소를 읽어들이는 것
- slicing : 요소의 특정 부분을 따로 분리해 조작하는 것

<br>

## 사용법

```java
int[] arr = new int[10];
String[] strArr = {"a","b","c","d"};

Arrays.fill(arr, 100);             // 배열의 요소를 모두 같은 값으로 초기화
arr[0] = 99;                       // 값 할당

System.out.println(arr[0]);        // 값 가져오기
System.out.println(strArr.length); // 배열의 길이
```


<br>

## 활용

- 데이터의 개수가 확실하게 정해져 있을 때
- 데이터의 삽입/삭제가 빈번하지 않을 때
- 검색을 해야할 때

<br><br>

# 📍 ArrayList

![image](https://user-images.githubusercontent.com/78673570/183255383-815cc70d-ead0-4fcf-bd63-639033304cbb.png)

- 길이를 동적으로 변경할 수 있는 `List`의 특징을 가진 배열

&nbsp; &nbsp; &nbsp; &nbsp;
💡 Array에서는 '인덱스'가 중요했다면, List에서는 '순서'가 중요하다. (List = sequence = '순서'가 있는 데이터의 모임)

<br>

## 특징

### 1. 동적으로 사이즈를 변경할 수 있다.

Array와의 가장 큰 차이이다. 크기가 정해져있지 않기 때문에, 중간에 요소를 삽입/삭제하더라도 Array에서 갖고 있던 문제점을 해결할 수 있다.

> ❗ 요소의 삽입/삭제 시 빈 공간을 메꾸기 위해 기존의 요소들이 이동해야하기 때문에, 삽입/삭제가 반복적으로 일어나게 된다면 성능적인 이슈가 발생할 수 있다.

<br>

### 2. Array의 특징

- 빠른 검색 성능 ('인덱스'를 통해 데이터를 관리한다.)
- 데이터가 순차적으로 저장된다.

<br>

## 사용법

```java
ArrayList<Integer> integers = new ArrayList<Integer>(); // 타입 지정 선언
ArrayList<Integer> integers = new ArrayList<>();        // 타입 생략 선언
ArrayList<Integer> integers = new ArrayList<>(10);      // 초기 용량(Capacity) 설정

integers.add(10);                                       // 값 추가
integers.get(0);                                        // 특정 인덱스의 값 가져오기
integers.set(0, 100);                                   // 값 수정
integers.remove(0);                                     // 값 삭제 - '인덱스'를 통해 삭제
integers.remove(Integer.valueOf(20));                   // 값 삭제 - '값'을 통해 삭제

integers.clear();                                       // 배열 전체 삭제
integers.removeAll(Arrays.asList(Integer.valueOf(1)));  // 특정 element를 모두 삭제

Collections.sort(integers);                             // 오름차순 정렬
Collections.sort(integers, Collections.reverseOrder()); // 내림차순 정렬

integers.contains(3);                                   // 특정 element 존재 여부 확인

```
<br>

## 활용

- 크기가 정해져 있지 않을 때
- 데이터의 삽입/삭제가 빈번하지 않을 때
- 검색을 해야할 때

<br><br>

# 📍 LinkedList

![image](https://user-images.githubusercontent.com/78673570/183255394-c7635ec7-4a87-4a64-b80d-0b1fdc4161d1.png)

- 요소(element)와 요소(element) 간의 연결(link)을 이용해서 리스트를 구현한 것
- 데이터를 저장하는 각 노드가 이전 노드와 다음 노드의 상태만 알고 있는 자료

<br>

## 특징

### 1. 요소의 삽입/삭제가 빠르다.

요소를 중간에 삽입/삭제하더라도 전체를 돌지 않고, 이전 값과 다음 값이 가리켰던 주소값만 수정하여 연결시키기 때문에 빠르게 진행할 수 있다.

<br>

### 2. 순차 접근만 가능하다.

인덱스를 갖고 있지 않기 때문에, 처음부터 순차적으로 살펴봐야한다. 따라서 검색에 있어서는 시간이 더 오래 걸린다.


<br>

### 3. 추가적인 저장 공간이 필요하다.

다음 노드를 가리키는 포인터를 저장하기 위한 공간이 추가적으로 필요하다.

<br>

## 사용법

```java
LinkedList<Integer> integers = new LinkedList<Integer>(); // 타입 지정 선언
LinkedList<Integer> integers = new LinkedList<>();        // 타입 생략 가능

integers.add(10);                                         // 값 추가
integers.addFirst(0);                                     // 맨 앞에 값 추가
integers.addLast(99);                                     // 맨 마지막에 값 추가
integers.get(0);                                          // 특정 인덱스의 값 가져오기
integers.set(0, 100);                                     // 값 수정
integers.remove();                                        // 값 삭제 - 첫 번째 값 제거

integers.clear();                                         // 전체 삭제
integers.contains(3);                                     // 특정 element 존재 여부 확인

```

<br>

## 활용

- 크기가 정해져 있지 않을 때
- 데이터의 삽입/삭제가 빈번할 때
- 검색을 자주 하지 않을 때

<br><br>

# 📍 Array vs ArrayList vs LinkedList

- 데이터의 크기가 정해져있지 않다면 `ArrayList`, `LinkedList`를 사용하는 것이 좋다.
- 삽입/삭제가 빈번하다면 `LinkedList`를 사용하는 것이 좋다.
- 데이터에 빠르게 접근하는 게 중요하다면 `Array`, `ArrayList`를 사용하는 것이 좋다.

<br>

## 시간 복잡도

| &nbsp; | ArrayList | LinkedList | 
| ------ | :-------: | :--------: |
| get / set	| O(1) | O(n) |
| add (시작)	| O(n) | O(1) |
| add (끝) | O(1) | O(1) |
| add (일반)	| O(n) | O(n) |
| remove (시작) | O(n) | O(1) |
| remove (끝)	| O(1) | O(1) |
| remove (일반) | O(n) | O(n) |

<br>

`get/set`  
- ArrayList : 인덱스를 통해 바로 접근한다. / 상수 시간 O(1)
- LinkedList : 시작이나 끝에서부터 해당 인덱스까지 순차적으로 접근한다. / O(n)

<br>

`add`
- ArrayList
    - 데이터를 중간에 add 할 경우, 해당 요소 뒤에 있는 모든 요소의 자리 이동해야한다. / O(n)
    - 데이터를 맨 끝에 add 할 경우, 바로 삽입한다. / O(1)
- LinkedList
    - 데이터를 중간에 add 할 경우, 데이터를 추가할 인덱스까지 순차적으로 접근한다. / O(n)
    - 데이터를 맨 앞이나 맨 끝에 add 할 경우, 바로 ㅅ바입한다. / O(1)

<br>

`remove`
- ArrayList
    - 중간의 데이터를 remove 할 경우, 해당 요소 뒤에 있는 모든 요소의 자리 이동해야한다. / O(n)
    - 맨 끝의 데이터를 remove 할 경우, 바로 삭제한다. / O(1)
- LinkedList
    - 중간의 데이터를 remove 할 경우, 데이터를 추가할 인덱스까지 순차적으로 접근한다. / O(n)
    - 맨 앞이나 맨 끝의 데이터를 remove 할 경우, 바로 삭제한다. / O(1)
