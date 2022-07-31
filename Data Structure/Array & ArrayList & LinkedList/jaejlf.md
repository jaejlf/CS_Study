## 📍 배열(Array)

![image](https://user-images.githubusercontent.com/78673570/182015583-18e5de2f-3781-4cd1-b537-bdfa5858ce16.png)

= 각각의 값(value)에 인덱스(index)를 부여해서 해당 데이터를 불러오는 자료구조 <br>
= '인덱스'를 호출하면 해당 인덱스에 저장되어있는 '값'이 나온다. <br>
= 동일한 자료형의 데이터를 연속된 공간에 저장하기 위한 자료구조 (연관된 데이터를 그룹화하여 묶어주는 것) <br>
= 선형 자료구조 (sequence container)

<br>

### 특징
-   stack에 메모리가 할당된다.
-   메모리의 연속성 : 배열은 메모리가 순차적으로 저장되기 때문에 어느 위치에 있는지 인덱스로 쉽게 접근할 수 있는다.  
    (= 순차 접근(sequential access)이 Linked List보다 빠르다)
-   동일한 자료형 : 선언될 때 모든 칸에 있는 값들은 동일한 type으로 선언된다.
-   중복 허용 : 값의 중복을 허용하는 자료형이다.
-   불변 길이 : 메모리 할당 시 길이를 늘릴 수 없다. 즉, 사용하지 않는공간이라도 해당 메모리 공간을 차지하고 있기 때문에 메모리가 낭비될 수 있다.
-   빠른 검색 성능 : '인덱스'를 사용하기 때문에 무작위 접근(random access)가 가능하여 검색 성능이 빠르다.
-   값의 추가/삭제가 오래 걸린다 : 값을 중간에 추가/삭제할 경우 해당 엘리먼트 뒤에 있는 모든 엘리먼트의 자리 이동이 필요하다.  
    (=> 삽입/삭제가 빈번하게 발생하는 프로세스의 경우 치명적)

<br>

### 시간 복잡도

-   삽입/삭제
    -   배열의 맨 앞에 삽입/삭제하는 경우 : O(n)
    -   배열의 맨 뒤에 삽입/삭제하는 경우 : O(1)
    -   배열의 중간에 삽입/삭제하는 경우 : O(n)
-   탐색 (인덱스 접근) : O(1)

<br>

### 사용법

```java
int[] odds = {1, 3, 5, 7, 9};
String[] weeks = {"월", "화", "수", "목", "금", "토", "일"};

odds.length; // 배열의 길이
```

<br>

### 활용 예시

-   데이터 개수가 확실하게 정해져 있을 때
-   데이터의 삭제와 삽입이 적을 때
-   검색을 해야할 때


<br><br>

## 📍 ArrayList

### Array vs ArrayList

`공통점`

-   '인덱스'를 통해 데이터를 관리한다.
-   연속된 메모리 공간을 사용한다.

<br>

`차이점`

-   ArrayList는 heap에 메모리가 할당된다. (new 키워드를 사용해 생성)
-   ArrayList는 Array와 달리 크기를 동적으로 늘릴 수 있다.
-   자료형
    -   Array : primitive type (int, string 등), object type
    -   ArrayList : object element  
        (ex. int는 기본 자료형이기 때문에, int를 객체화 시킨 wrapper클래스인 'Integer'을 사용해야한다.)

<br>

### 사용법

```java
ArrayList<Integer> integers = new ArrayList<Integer>(); // 타입 지정 선언
ArrayList<Integer> integers = new ArrayList<>();        // 타입 생략 선언
ArrayList<Integer> integers = new ArrayList<>(10);      // -> 초기 용량(Capacity) 설정

integers.add(10);                     // 값 추가
integers.get(0);                      // 특정 인덱스의 값 가져오기
integers.set(0, 100);                 // 값 수정
integers.remove(0);                   // 값 삭제 - '인덱스'를 통해 삭제
integers.remove(Integer.valueOf(20)); // 값 삭제 - '값'을 통해 삭제

integers.clear();                                      // 배열 전체 삭제
integers.removeAll(Arrays.asList(Integer.valueOf(1))); // 특정 element를 모두 삭제

Collections.sort(integers);                              // 오름차순 정렬
Collections.sort(integers, Collections.reverseOrder());  // 내림차순 정렬

integers.contains(3); // 특정 element 존재 여부 확인
```

<br><br>

## 📍 LinkedList

= element와 element 간의 연결(link)을 이용해서 리스트를 구현한 것 <br>
= 선형 자료구조 (sequence container)

<br>

### 특징

-   heap에 메모리가 할당된다. (new 키워드를 사용해 생성)
-   값의 추가/삭제가 빠르다 : 추가/삭제가 될 값의 이전/이후 노드의 참조값만 변경하면 된다.
-   크기가 가변적이다 : 새로운 값을 추가할 경우 동적으로 크기가 변경된다.
-   불연속적인 메모리 할당 : 빈 공간없이 데이터를 저장할 수 있다.
-   저장 공간의 낭비 : 다음 노드를 가리키는 포인터를 저장하는공간이 추가적으로 필요하다.

<br>

### 시간 복잡도

-   삽입
    -   리스트의 맨 앞/뒤에 삽입하는 경우 : O(1)
    -   리스트의 중간에 삽입하는 경우 : O(n) (= 탐색하는 시간)
-   삭제
    -   리스트의 맨 앞/뒤에서 삭제하는 경우 : O(1)
    -   리스트의 중간에서 삭제하는 경우 : O(n) (= 탐색하는 시간)
-   탐색 : O(n)

<br>

### 사용법

```java
LinkedList<Integer> integers = new LinkedList<Integer>(); // 타입 지정 선언
LinkedList<Integer> integers = new LinkedList<>();       // 타입 생략 가능

integers.add(10);      // 값 추가
integers.addFirst(0);  // 맨 앞에 값 추가
integers.addLast(99);  // 맨 마지막에 값 추가
integers.get(0);       // 특정 인덱스의 값 가져오기
integers.set(0, 100);  // 값 수정
integers.remove();     // 값 삭제 - 첫 번째 값 제거

integers.clear();      //  전체 삭제

integers.contains(3); // 특정 element 존재 여부 확인
```

<br>

### 활용 예시

-   크기가 정해져 있지 않을 때
-   삽입과 삭제가 자주 일어날 때
-   검색을 자주 하지 않을 때
