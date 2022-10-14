# 💡 Redis

## Redis 란?

![](https://velog.velcdn.com/images/wisdom-one/post/faff5028-2a6c-4a9f-b4d3-c0f947ae2e60/image.png)

<br/>

"**Re**mote **Di**ctionary **S**erver"

Redis는 `데이터베이스` , `캐시` , `메시지 브로커` , `스트리밍 엔진` 으로 사용되는 인메모리 data structure store 이다.

메모리에서 데이터를 처리하기 때문에 작업 속도가 상당히 빠르다.

또한 `Key-Value` 형태로 데이터를 저장하기 때문에 쿼리를 날리지 않고도 결과를 얻을 수 있어 속도가 빠르다.

인 메모리로 동작하지만, 정기적으로 데이터셋을 Disk에 dump하거나 각 명령을 Disk 기반 로그에 추가하여 데이터를 유지(`영속화`)할 수 있다.


### 특징

- `영속성` 을 지원하는 인 메모리 데이터 저장소
- 다양한 자료 구조를 지원
- `싱글 스레드` 방식으로 인해 연산을 원자적으로 수행 가능 (`thread safe`)
- 읽기 성능 증대를 위한 서버 측 `리플리케이션(Replication)` 지원
- 쓰기 성능 증대를 위한 클라이언트 측 `샤딩(Sharding)` 지원
- 다양한 서비스에서 사용되며 검증된 기술

<br/>

## 영속성 (persistence)

Redis는 인메모리로 동작함에도 불구하고 어떻게 영속성을 지원할까?

Redis에서는 4가지 영속성 옵션을 제공한다.

1. RDB (Redis Database) : 지정된 간격(interval)마다 그 시점의 datasest 스냅샷을 수행한다. 즉 현재 메모리에 저장된 데이터 상태들을 특정 시점에 디스크에 저장(백업)한다.
2. AOF (Append Only File) : 서버가 수신한 모든 write 작업을 기록하고, 서버 재시작 시 이 작업들이 실행되어 dataset을 재구축한다.
3. No persistence : 원하는 경우, 영속성(지속성)을 완전히 비활성화할 수 있다.
4. RDB + AOF : 동일한 인스턴스에서 AOF와 RDB를 결합하여 사용한다. 주기적으로 snapshot으로 백업하고, 다음 snapshot까지의 저장을 AOF 방식으로 수행하는 방식으로 혼용해서 사용한다.

<br/>

> 자세한 내용은 [공식문서](https://redis.io/docs/manual/persistence/) 참고.

<br/>

## 데이터 타입

value에는 다양한 데이터 타입이 존재한다.

![](https://velog.velcdn.com/images/wisdom-one/post/0579984b-6856-47ff-94e3-7478d98e69a1/image.png)

- Strings : 문자열이나 숫자
- Lists : 리스트 (중복 원소 가능)
- Sets : 집합 (중복 원소 불가능)
- Hashes : key/value 목록
- Sorted sets : 정렬 집합
- Streams
- Geospatial indexes
- Bitmaps
- Bitfields
- HyperLogLog

<br/>

> 자세한 내용은 [공식문서](https://redis.io/docs/data-types/)를 참고.


<br/>

## Redis vs Memcached 

`Memcached` 또한, 인 메모리 기반의 캐싱 시스템으로써, 데이터를 key-value 형태로 저장한다는 점에서 Redis와 유사하다.

그렇다면 `Redis` 와 `Memcached` 의 차이점은 무엇일까?

<br/>

| |Redis|Memcached
--|:--:|:--:
스레드| 싱글 스레드 | 멀티 스레드
자료구조 | string, list, hash, set 등 다양한 자료구조 지원 | string 과 integer 만 지원
데이터 저장| Memory, Disk | Only Memory
처리 속도|Memcached 보다는 느리지만 큰 차이는 없음|디스크를 거치지 않아 Redis보다 빠름
Replicatioin|지원|미지원
Partitioning method|지원|미지원
영속성(Persistence)|지원|미지원




<br/><br/>

## 🔖 참고
- [블로그](https://steady-coding.tistory.com/586)
