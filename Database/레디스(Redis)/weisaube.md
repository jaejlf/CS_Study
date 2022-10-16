# 레디스(Redis)

## 📌 A. 레디스

> REmote DIctionary Server의 약어로, 빠른 오픈 소스 인 메모리 키 값 데이터 구조 스토어

### Redis의 특징

1. Remote에 위치한
2. 프로세스로 존재하는
3. In-Memory: 메모리 기반의
4. "키-값" 구조 데이터 관리 시스템
   - 비관계형이며, 키-값 구조이기 때문에 별도 쿼리 없이도 데이터를 간단히 가져올 수 있다

<br/>

#### Redis가 지원하는 자료구조

- String
- Set
- Sorted Set
- Hash
- List

<br/>

Redis는 특성이나 상황에 따라 위의 자료구조를 **1)캐시** 로 사용할 수도 있고, **2)Persistence**로 사용할 수도 있다.

<br/>

## 📌 B. 캐시로 사용

- 사용 이유: 나중에 요청된 결과를 미리 저장해두었다가 빨리 제공하기 위해 사용

<br/>

Redos Cache는 메모리 단(In-Memory)에 위치한다.

따라서 디스크보다 수용력(용량) 은 적지만 접근 속도는 빠르다.

<br/>

### 캐시의 사용 방법

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fhyeondev%2Fpost%2Fd13edf64-100b-412c-a5ea-af0c80ef2147%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-03%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.07.33.png" alt="text" width="485" />
</p>

<br/>

- 일반적인 패턴: `Look Aside Cache`

  1. 웹 서버는 클라이언트 요청을 받아, 데이터가 존재하는지 **캐시를 먼저 확인**
  2. - Cache에 데이터 존재:
       → Cache에서 데이터 추출
     - Cache에 데이터 존재하지 않음 → DB에서 읽어온 후 캐시에 이를 저장한 다음 클라이언트에게 데이터를 돌려줌

- `Write Back`
  - 데이터를 캐시에 전부 먼저 저장해놓았다가 특정 시점마다 한번씩 캐시 내 데이터를 DB insert 하는 방법
  - 단점:
    - 데이터를 일정 기간동안은 유지하고 있어야 하는데, 이때 이걸 유지하고 있는 storage 는 메모리 공간이므로 서버 장애 상황에서 데이터가 손실될 수 있음
- 극단적으로 heavy한 데이터에서 `write back` 방식 사용

<br/>

### 장점

- 메모리 캐시로 인해 엑세스 지연 시간을 줄이고 처리량을 늘릴 수 있음
- 관계형 또는 NoSQL 데이터베이스의 부담을 줄여줌

<br/>

## 📌 B. Redis의 특징

> Collection을 제공함

<br/>

### Collection의 장점

<br/>

#### Case1. 대상 사용자가 많은 경우 랭킹을 산출하는 서버를 구현시

- Redis 의 Sorted Set 을 사용하면 랭킹 서버를 쉽게 구현 가능하며 replication 까지도 가능

<br/>

#### Case2. 친구 리스트를 관리할 때 데이터를 key-value 형태로 저장해야 한다면

- 같은 친구 리스트를 읽은 후 서로 다른 클라이언트에서 리스트에 서로 다른 친구를 추가하려 했을 시
  - 친구 리스트의 최종 상태는 -> 두 클라이언트가 추가한 사람 A, B 가 전부 반영되지 않을 수 있다. (`race condition`)

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fhyeondev%2Fpost%2F6fafd94a-3b9e-4727-959a-4af2ea5cde60%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-03%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.49.40.png" alt="text" width="485" />
</p>

<br/>

T1[친구 B 추가] -> T2[친구 C 추가] -> T1[B 추가한걸 최종상태에 반영(쓰기)] -> T2[C 추가한걸 최종상태에 반영(쓰기)]

3번째와 4번째 프로세스가 순서대로 진행되면서 리스트 덮어쓰기가 발생하고, 최종 상태에서도 결국 context switching 때문에 T1 과 T2 둘 중 뭐가 먼저 발생할지 예측할 수 없다는 문제 존재<br/>
친구리스트가 [A,B] or [A,C] 랜덤으로 유지될 수 있다.

<br/>

👉 Redis 자료구조는 Atomic 하다는 특징 때문에 이런 race condition 을 피할 수 있다.

즉, Redis Transaction 은 한번의 딱 하나의 명령만 수행할 수 있다.

이에 더하여 single-threaded 특성 을 유지하고 있기 때문에 다른 스토리지 플랫폼보다는 이슈가 덜하다고 한다.

 <br/>

## 📌 D. 참고 자료

🔗[Redis란 무엇일까](https://velog.io/@hyeondev/Redis-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)
