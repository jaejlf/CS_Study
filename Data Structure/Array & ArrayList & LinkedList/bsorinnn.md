# Array & ArrayList & LinkedList

## A. Array란?

- Array = 배열
- 자료구조에서 배열은 연속된 메모리 공간에 순차적으로 저장된 데이터 콜렉션
- 선언 시 **크기와 데이터 타입**을 지정해야 한다.

```C
// 크기가 10인 Int 형 배열 선언
int numArr[10]
```

- `O(1)`에 k번째 원소에 접근 가능하다.
- 추가적으로 소모되는 메모리의 양(=overhead)가 거의 없다.
- Cache hit rate가 높다.
- 배열이 제공하는 기능
  - 임의의 위치에 있는 원소를 확인/변경 → `O(1)`
  - 마지막 원소 추가/제거 → `O(1)`
  - 임의의 위치에 원소 추가/제거 → `O(N)`
    - 뒤에 위치한 원소들을 전부 한 칸씩 밀어야/당겨와야 하므로

<img src="https://www.nextree.co.kr/content/images/2021/01/jdchoi_20140225_arrayvslinkedlist11.png" height = 100>

## B. LinkedList란?

### 1. List

- 리스트(List): LinkedList, ArrayList 등 선형 자료 구조를 구현할 때 사용되는 추상 자료형
  - 같은 특성을 같는 원소들이 순서대로 구성
  - 데이터가 메모리 상 연속적으로 저장되어 있지 않다(실제 메모리 주소 랜덤)
    - 따라서 Cache Hit Rate 낮다
  - 크기 가변적
  - 시간복잡도
    - 원소 접근 → `O(N)`
    - 원소 삽입 / 삭제 → `O(N)`

### 2. LinkedList

- 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있다.
- 포인터는 다음/이전 노드의 주소를 담고 있다.
- k번째 원소를 확인하기 위해서는 `O(K)` 필요
- 원소들이 메모리에 연속해있지 않아 Cache Hit Rate는 낮지만 할당은 쉽다
- 크기가 **가변적**이다
- 연결 리스트가 제공하는 기능
  - 임의의 위치에 있는 원소를 확인/변경 → `O(N)`
    - 그 위치에 도달할 때까지 첫 번째부터 순차적으로 방문
  - (추가하고 싶은 위치의 주소를 알고 있을 경우) 임의의 위치에 원소 추가/제거 → `O(1)`
    - 주소만 변경해주면 되므로
- 연결 리스트의 종류
  - 단일 연결 리스트(Singly Linked List)
  - 원형 연결 리스트(Circular Linked List)
  - 이중 연결 리스트(Doubly Linked List)

## C. ArrayList란?

- JAVA에서는 Collection 프레임워크의 일부
- ArrayList는 **크기가 가변적인 배열**
- 내부적으로는 array로 이루어져 있기 때문에 index를 가짐
- ArrayList가 제공하는 기능
  - 임의의 위치에 있는 원소를 확인/변경 → `O(1)`
  - 임의의 위치에 원소 추가/제거 → `O(N)`
    - 뒤에 위치한 원소들을 전부 한 칸씩 밀어야/당겨와야 하므로

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcJFemK%2FbtroM6XXMAW%2F7CBVQIsIQTwTQQ4OtDIKaK%2Fimg.png" height = 250>

[출처] [[자료구조] Array(배열) vs List(리스트) - 옹벨 일기](https://ongveloper.tistory.com/403)

## D. Array in Swift

Apple Developer Documentation에서는 Array를 '정렬되며, 랜덤으로 접근 가능한 콜렉션'으로 정의한다.

> +) Swift에서 콜렉션이란?

> Swift에서는 콜렉션 타입으로 `배열(array)`, `세트(Set)`, `딕셔너리(Dictionary)` 세 가지를 지원한다.

- Array는 단일 데이터 타입을 저장한다.
- 정수(Integer), 문자열(String), 클래스(Class)까지 다양한 데이터 타입을 저장할 수 있다.
- Swift의 배열은 선언 시 **크기를 지정하지 않아도 된다.**
- 빈 배열 생성 시 Element의 데이터 타입을 지정해줘야 한다.

```Swift
// Shortened forms are preferred
var emptyDoubles: [Double] = []

// The full type name is also allowed
var emptyFloats: Array<Float> = Array()
```

- 기본값으로 빈 배열 생성 시 `Array(repeating:count:)` 이니셜라이저를 사용한다.

### 1. 배열에 접근하기

- `isEmpty` 프로퍼티: 배열의 원소가 있는지 확인
- `count` 프로퍼티: 배열의 원소 개수
- `first/last` 프로퍼티: 배열의 첫번째 원소/마지막 원소에 safe access 할 수 있게 해준다(배열이 비어있을 경우 `nil`)
- 서브스크립트(subscript)로 각각의 원소에 접근 가능
  - 비어 있지 않은 배열의 첫번째 요소는 항상 인덱스 0으로 접근 가능
  - 0 ~ 배열의 개수 - 1
  - 배열의 개수보다 크거나 음수 인덱스 사용 시 런타임 에러 발생

> subscript란?

> 서브스크립트란 콜렉션, 리스트, 시퀀스 등 집합의 특정 멤버 엘리먼트에 간단하게 접근할 수 있는 문법

### 2. 배열 추가/삭제

- `append(_:)`: 배열의 마지막에 원소 하나 추가
  - 시간복잡도: 평균 - `O(1)`, 최악 - `O(N)`
- append(contentsOf:) : 배열의 마지막에 다른 배열이나 시퀸스 추가
  - 시간복잡도: 평균 - `O(N)`
- insert(\_:at:): at이 가리키는 인덱스에 원소 추가
  - 시간복잡도: `O(N)`
- `remove(at:), removeSubrange(\_:), removeLast()'`: 배열에서 원소 삭제

### 3. 배열의 크기 수정

(C++의 Vector와 유사)

- Swift Array는 초기에 적당한 양의 메모리 할당해놓음
- 그러나 원소 추가 시 배열의 크기 벗어날 경우 메모리 재할당 필요
- `capacity`: 새로운 스토리지 할당 없이 배열에 얼마만큼의 element를 담을 수 있는지
  - 더 큰 메모리 영역을 할당하고 해당 원소들을 새 스토리지에 복사
- 새 스토리지는 이전 스토리지 크기(capacity)의 배수
- 지수 성장(expotional growth) 정책
- 재할당 추가 작업은 비용이 많이 들지만 배열이 커질수록 발생하는 빈도는 점점 줄어듦
- 저장해야 하는 원소 개수를 대략적으로 알고 있을 경우 `reserveCapacity(_:)`로 용량 예약하고 중간에 재할당 일어나는 것 막을 수 있음

### 4. 배열 복사

- Element가 값 타입일 경우 복사한 배열에서 값 변경해도 원본 배열에서는 바뀌지 않음
- Element가 클래스와 같이 참조 타입일 경우 복사한 배열에서 값 변경 시 원본 배열에도 영향
  - 클래스의 새로운 인스턴스 할당 해 서로 다른 주소 참조하게 하면 더 이상 영향 받지 않음
- Swift의 Array는 Copy-On-Write(COW) 사용
- array의 복사본들은 변경되기 전까지 같은 스토리지 공유
  - 수정 일어날 시 그때 복사

## E. 참고자료

🔗 https://ongveloper.tistory.com/403

🔗 https://demian-develop.tistory.com/30

🔗 https://sujinnaljin.medium.com/swift-array-%EC%9D%98-capacity-9c3a99d2c31f

🔗https://developer.apple.com/documentation/swift/array
