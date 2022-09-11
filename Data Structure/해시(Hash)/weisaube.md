# 해시(Hash)

> 키(key)와 값(Value) 쌍으로 이루어진 데이터 구조

<br>

해시 구조에서는 키(key)를 이용해서 데이터(Value)를 빠르게 찾을 수 있다.

<br>

## A. 용어 정리

<img src="https://velog.velcdn.com/post-images%2Fcyranocoding%2F8d25f580-b225-11e9-a4ce-730fc6b3757a%2F1iHTnDFd3sR5FqjHD1FDu9A.png">

<br>

- `키(key)`: 해시 함수의 input이 되는 고유한 값

키는 해시 함수(hash function)을 통해 해시로 변경되어 value 값과 매칭되어 저장소에 저장된다

- `해시(Hash)`: 임의의 값을 고정 길이로 변환하는 것

키값 그대로 저장소에 저장하게 되면 다양한 길이의 저장소를 구성해야 하기 때문에 효율성을 위해 일관적으로 해시(hash)로 변경하여 저장

- `해시 테이블(Hash Table)`: 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조

- `버킷(Bucket)`, `슬롯(Slot)`: 해시 테이블에서 하나의 데이터가 저장되는 공간

- `해시 함수(Hashing Function)`: 키 값에 대한 연산을 통해 데이터의 위치를 찾는 함수

- `Hash Value`, `Hash Address`: 키 값을 이용해 해시 함수를 연산하여 value를 알아낼 수 있고, 이를 기반으로 해시 테이블에서 해당 키에 대한 데이터 위치(주소)를 알아낼 수 있다.

<br>

## B. 해시 테이블 기능

<br>

### 데이터 삽입(저장)

<br>

<과정>

1. 해시 함수를 이용하여 키 값을 해시로 변경
2. 미리 준비해둔 저장소(bucket, slot) 중 알맞는 hash 값을 찾아 value를 저장한다.

- 시간복잡도: (해시 충돌이 일어나지 않는다는 가정 하에) `O(1)`

<br>

### 데이터 삭제

<br>

bucket에서 삭제하려고 하는 key와 매칭되는 value 값을 찾아서 삭제

- 시간복잡도: (해시 충돌이 일어나지 않는다는 가정 하에) `O(1)`

<br>

### 데이터 검색

<br>

key를 이용해 value를 찾아내는 과정

<과정>

1. key 값과 hash function을 이용해 hash 찾아내기
2. 해당 hash로 value 찾기

- 시간복잡도: (해시 충돌이 일어나지 않는다는 가정 하에) `O(1)`

<br>

## C. Hash Table 장단점

<br>

- 장점: 데이터 저장, 삭제, 검색 모두 시간복잡도가 `O(1)`
- 단점:
  - hash 값을 저장할 공간(bucket)을 저장해야 하므로 저장 공간이 많이 필요함
  - 여러 키에 해당하는 hash(주소)기 동일한 경우에는 `해시 충돌(Hash Collision)`이 발생할 수 있음

<br>

## D. 해시 충돌(Hash Collision)

<br>

> 여러 key 에 해당하는 hash(주소)가 동일한 경우

<br>

해시 충돌을 해결하기 위한 여러 방법들

### 1. Chaning(Open Hashing)

<br>

연결 리스트를 이용하는 방식인 Chaining 방법을 이용해 해시 충돌 문제를 해결할 수 있다.

<br>

<img src="https://user-images.githubusercontent.com/84179578/159212644-fd16d299-1fd5-452f-914f-f001a2a66589.png">

<br>

Sandra에게 충돌이 발생하자 기존에 있던 John의 값에 연결시킨다.

- Chaining: 저장 시 저장소(bucket)에서 충돌이 발생하면 해당 값을 기존의 값과 연결시키는 기법

이때 연결 리스트(linked list)를 이용하여 다음에 저장된 자료를 기존의 자료 다음에 위치시킨다.

<br>

#### Chaining의 장단점

<br>

- 장점:
  - 한정된 저장소를 효율적으로 사용할 수 있다
  - 해시 함수를 선택하는 중요성이 상대적으로 적다
  - 상대적으로 적은 메모리를 사용한다
- 단점:
  - 한 해시에 자료들이 계속 연결된다면(쏠림 현상) 검색 효율이 낮아진다
  - 외부 저장 공간을 사용한다
  - 외부 저장 공간 작업을 추가로 해야 한다

<br>

#### Chaining 시간복잡도

<br>

- 테이블 저장소(Bucket)의 길이: n
- 키의 수: m

평균적으로 저장소에는 1개의 해시당 (m/n)개의 키가 들어가 있다.

```
m/n = a
```

<br>

- 삽입
  - Head에 자료 저장: `O(1)`
  - Tail에 자료 저장: `O(a)`
  - 최악의 경우: `O(n)`
- 삭제&검색
  - `O(a)
  - 최악의 경우: `O(n)`

<br>

### 2. Open Addressing

<br>

> 비어있는 해시(hash)를 찾아 데이터를 저장하는 기법

Chaining과 달리 1개의 해시와 1개의 값이 매칭되어 있는 형태로 유지

<img src="https://velog.velcdn.com/post-images%2Fcyranocoding%2F7c9f8040-b226-11e9-89af-8fc0a61dbc3e%2F19O8Eyd9wEhZKhwrXzKJaw.png">

Sandra 저장될 때 해시가 John으로 채워져 있어 그 다음 Hash에 Sandra 저장

이 때, 비어있는 해시(Hash)를 찾는 과정은 동일해야 한다.(일정한 규칙을 따라 찾아가야 한다.)

Open Addressing은 비어있는 해시를 찾는 규칙에 따라 다음과 같이 구분할 수 있다:

- 선형 탐색(Linear Probing): 다음 해시(+1)나 n개(+n)를 건너뛰어 비어있는 해시에 데이터를 저장한다.
- 제곱 탐색(Quadratic Probing): 충돌이 일어난 해시의 제곱을 한 해시에 데이터를 저장한다.
- 이중 해시(Double Hashing): 다른 해시함수를 한 번 더 적용한 해시에 데이터를 저장한다.

<br>

#### Open Addressing의 장단점

<br>

- 장점:
  - 또 다른 저장공간 없이 해시테이블 내에서 데이터 저장 및 처리가 가능하다
  - 또 다른 저장공간에서의 추가적인 작업이 없다
- 단점:
  - 해시 함수(Hash Function)의 성능에 전체 해시테이블의 성능이 좌지우지된다
  - 데이터의 길이가 늘어나면 그에 해당하는 저장소를 마련해 두어야 한다

<br>

#### Open Addressing의 시간복잡도

<br>

해시 테이블의 저장소(Bucket)의 길이를 ’n’, 키(key)의 수를 ‘m’이라고 가정했을 때, ‘α’는 1보다 작거나 같다. 저장소 1개 버킷 당 1개의 값(value)만 가지기 때문이다.

```
m/n = α (α <= 1)
```

- Insertion & Deletion& Search:
  - 최상의 경우:`O(1)`
  - 최악의 경우: `O(n)`

삽입, 삭제, 검색 모두 대상이 되는 Hash를 찾아가는 과정에 따라 시간복잡도가 계산이 된다.

해시함수를 통해 얻은 Hash가 비어있지 않으면 다음 버킷을 찾아가야 한다.

이 찾아가는 횟수가 많아지면 많아질 수록 시간복잡도가 증가한다.
