# 💡 해시(Hash)

## 1. 정의

**해시함수(hash function)** 란?

데이터의 효율적 관리를 목적으로 임의의 길이의 데이터를 **고정된 길이**의 데이터로 매핑하는 함수.

이 때 매핑 전 원래 데이터의 값을 `키(key)`, 매핑 후 데이터의 값을 `해시값(hash value)`, 매핑하는 과정 자체를 `해싱(hashing)` 이라고 한다.

<br/>

**해시 테이블(hash table)** 이란?

해시함수를 사용하여 키를 해시값으로 매핑하고, 이 해시값을 색인(인덱스) 또는 주소 삼아 데이터를 key와 함께 저장하는 자료구조. 

행(row)를 버켓(bucket)이라고 하고 열(column)을 슬롯(slot)이라고 한다.


<img style="margin:0 auto; width:400px" src="https://velog.velcdn.com/images/wisdom-one/post/18706371-d7e4-4b38-ba06-43206cb7e857/image.png" />

<br/>

## 2. 충돌 (collision)

두 개의 서로 다른 데이터가 해시 테이블의 같은 버켓 주소로 매핑되는 것을 `충돌(collision)`이라고 한다.

아래 그림에서는 Johb Smith와 Sandra Dee가 해시값이 02로 동일하여 충돌이 발생한다.

![](https://velog.velcdn.com/images/wisdom-one/post/77c82ade-5751-4c09-a4ce-2b95a7037451/image.png)

### 해결 방법

#### 1. 체이닝 (Chaining)

연결리스트로 노드를 계속 추가해나가는 방식 (제한 없이 계속 연결 가능, but 메모리 문제)

<br/>
    
장점
- 한정된 저장소(Bucket)을 효율적으로 사용할 수 있다.
- 해시 함수(Hash Function)을 선택하는 중요성이 상대적으로 적다.
- 상대적으로 적은 메모리를 사용한다. 미리 공간을 잡아 놓을 필요가 없다.

단점
- 한 Hash에 자료들이 계속 연결된다면(쏠림 현상) 검색 효율을 낮출 수 있다.
- 외부 저장 공간을 사용한다.
- 외부 저장 공간 작업을 추가로 해야 한다.

<br/>

#### 2. 개방주소법 (Open Addressing)

해시 함수로 얻은 주소가 아닌 다른 주소에 데이터를 저장할 수 있도록 허용하는 방식. 해당 버킷에 값이 저장되어 있으면 다음 주소에 저장한다. 

<br/>

장점
- 추가적인 저장공간 없이 해시테이블 내에서 데이터 저장 및 처리가 가능하다.
- 또 다른 저장공간에서의 추가적인 작업이 없다.

단점
- 해시 함수(Hash Function)의 성능에 전체 해시테이블의 성능이 좌지우지된다.
- 데이터의 길이가 늘어나면 그에 해당하는 저장소를 마련해 두어야 한다.

<br/>

Open Addressing 의 종류

- 선형 탐색 (Linear probing) : 다음 해시(+1)나 n개(+n)를 건너뛰어 비어있는 해시에 데이터를 저장한다.

- 제곱 탐색 (Quadratic Probing) : 충돌이 일어난 해시의 제곱을 한 해시에 데이터를 저장한다.

- 이중 해시(Double Hashing): 다른 해시함수를 한 번 더 적용한 해시에 데이터를 저장한다.


<br/>


## 3. 시간복잡도

해시 테이블은 key-value가 1:1 매핑되어 있기 때문에 검색, 삽입, 삭제 과정에서 모두 평균적으로 $O(1)$의 시간복잡도를 갖는다.

<br/>

## 🔖 참고
- [[자료구조] Hash의 개념 및 설명
](https://go-coding.tistory.com/30)
- [Hash, Hashing, Hash Table(해시, 해싱 해시테이블) 자료구조의 이해](https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o)
