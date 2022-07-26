# 📍 해시 (Hash)

키(key)와 값(value) 쌍으로 이루어진 데이터 구조

- `해시 함수(Hash Function)` : 데이터의 효율적인 관리를 목적으로 `임의의 길이의 데이터(= key)`를 `고정적인 길이의 데이터(= value)`로 `매핑`하는 함수
- 매핑 전 원래 데이터 값을 `키(key)`, 매핑 후 데이터 값을 `값(value)`이라고 하고, 매핑하는 과정 자체를 `해싱(hasing)`이라고 한다. 

<br>

## 해시 테이블 구성

### key

- 고유한 값, 해시 함수의 input
- key 값을 그대로 저장소의 인덱스로 사용할 경우, key의 길이만큼 정보를 저장해야 할 공간을 따로 마련해야하기 때문에 고정된 길이의 hash로 변경한다.

<br>

### value

- 저장소(버킷, 슬롯)에 최종적으로 저장되는 값
- hash와 매칭되어 저장된다.

<br>

### 해시 함수

- key를 고정된 길이의 hash로 변경해주는 역할

<br>

### 해시 테이블

- 해시 함수를 사용하여 key를 hash값으로 매핑하고, 이 hash값을 주소 또는 인덱스 삼아 value를 key와 함께 저장하는 자료구조
- 데이터가 저장되는 곳을 `버킷`, `슬롯`이라고 한다.

<br>

## 특징

### 장점

- 해시 테이블은 key-value가 1:1로 매핑되어 있기 때문에 삽입/삭제/검색의 과정에서 모두 평균적으로 `O(1)`의 시간복잡도를 가지고 있다.

<br>

### 단점

- 해시 충돌이 발생할 수 있다.
- 순서/관계가 있는 배열에는 어울리지 않는다.
- 데이터가 저장되기 전에 저장 공간을 미리 만들어두어야하므로, 채워지지 않는 공간이 발샏하는 등 공간 효율성이 떨어진다.
- 해시 함수의 의존도가 높다. (= 해시 함수가 복잡하다면 hash를 만들어 내는데 오래 걸린다.)

<br><br>

# 📍 해시 충돌 (Hash Collision)

- 서로 다른 key가 해싱 후 같은 값이 나오는 경우
- 해시 충돌 발생 확률이 적을수록 좋다.
- 해시 충돌이 균등하게 발생하도록 하는 것도 중요하다. 모든 키가 같은 해시값이 나오게 되면 데이터 저장 시 비효율성이 커지고 보안이 취약해져서 좋지 않다.

<br>

💡 Direct Address Table

= key의 전체 개수와 동일한 크기의 버킷을 가진 해시 테이블

key의 개수와 테이블의 크기가 같기 때문에 해시 충돌 문제가 발생하지 않는다.
하지만 실제 사용하는 key가 몇 개 되지 않을 경우 전체 key의 개수만큼 테이블의 크기를 유지하는 것은메모리 낭비이다.

<br>

## 체이닝(Chaining)

![image](https://user-images.githubusercontent.com/78673570/189358620-360debb2-bb02-454b-a3f3-643e6b903532.png)

- 버킷에서 충돌이 일어나면 기존 값과 새로운 값을 `연결 리스트`로 연결하는 방법
- 미리 충돌을 대비하여 공간을 많이 잡아놓을 필요가 없다. 충돌이 나면 그때 공간을 만들어서 연결만 해주면 된다.
- 같은 hash에 자료들이 많이 연결되면 검색 시 효율이 낮아진다.

<br>

## 개방 주소법(Open Addressing)

![image](https://user-images.githubusercontent.com/78673570/189359061-58972302-6754-4ed4-b744-57dd1198c4fb.png)

- 충돌이 일어나면 비어있는 hash에 데이터를 저장하는 방법
- hash와 value가 1:1 관계를 유지한다.

<br>

> 비어있는 hash 찾기
> 1. 선형 탐색 : 해시값에서 고정폭으로 건너 뛰면서 비어있는 해시가 나오면 저장한다.
> 2. 제곱 탑색 : 1 → 4 → 9 → ... 칸 씩 건너 뛰면서 빈 칸을 찾는다. 해시값이 같은 해시들이 들어오면 공간을 많이 확보해놔야 한다.
> 3. 이중 해싱 : 탐사할 해시값의 규칙성을 없애버려서 클러스터링을 방지하는 기법

<br><br>

# 📍 해시 함수 매핑 개선

특정값에 치우치지 않고 해시값을 고르게 만들어내는 해시 함수가 좋은 해시 함수라고 할 수 있다.

<br>

## division method

- 가장 기본적인 해시 함수
- 숫자로 된 key를 해시 테이블 크기 m으로 나눈 나머지를 해시값으로 변환한다.
- 간단하면서도 빠른 연산이 가능한 것이 장점이다.
- 해시의 중복을 방지하기 위해 테이블의 크기 m은 소수로 지정해서 사용하는 것이 좋다. 하지만 남는 공간이 발생해 메모리상으로 비효율적이다.

<br>

## multiplication method

- 숫자키 k, A는 0 < A < 1 사이의 실수 일 때 `h(k) = (k * a mod 1) * m`으로 계산한다.
- 2진수 연산에 최적화된 컴퓨터 구조를 고려한 해시 함수이다.

<br>

## univeral hasing

- 여러 개의 해시 함수를 만들고, 이 해시 함수의 집합 H에서 무작위로 해시 함수를 선택해 해시값을 만드는 기법
- 서로 다른 해시 함수가 서로 다른 해시값을 만들어내기 때문에, 같은 공간에 매핑할 확률을 줄이는 것이 목적
