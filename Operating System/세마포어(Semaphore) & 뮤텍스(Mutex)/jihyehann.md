# 💡 세마포어(Semaphore) & 뮤텍스(Mutex)

공유자원을 안전하게 관리하기 위해서는 `상호배제(Mutual exclusion)` 가 지켜져야 한다.

상호배제란, 한 번에 하나의 프로세스만이 임계영역에 들어가야 함을 의미하며 자세한 내용은 [이전 정리](https://github.com/jaejlf/CS_Study/blob/main/Operating%20System/Race%20Condition/jihyehann.md#%EC%83%81%ED%98%B8%EB%B0%B0%EC%A0%9C-mutual-exclusion)를 참고하자.

상호배제를 달성하기 위한 방법에는 `세마포어` 와 `뮤텍스` 가 있다.

<br/>

## 세마포어 (Semaphore)

### 세마포어란?
두 개의 원자적 함수로 조작되는 정수 변수로서, **멀티 프로그래밍 환경에서 공유 자원에 대한 접근을 제한하는 방법**으로 사용된다.

Dijkstra가 1965년에 제안한 개념으로, 식사하는 철학자(Dinning Philosopher) 문제의 고전적인 해법이지만 모든 교착 상태를 해결하지는 못한다.

<br/>

### 세마포어 P, V 함수

- P : 임계 구역 들어가기 전에 수행 (프로세스 진입 여부를 자원의 개수(S)를 통해 결정)
- V : 임계 구역에서 나올 때 수행 (자원 반납 알림, 대기 중인 프로세스를 깨우는 신호)

<br/>

### 구현
```
procedure P(S)   --> 최초 S값은 1임
    while S=0 do wait  --> S가 0이면 1이 될때까지 기다려야 함
    S := S-1   --> S를 0로 만들어 다른 프로세스가 들어 오지 못하도록 함
end P

--- 임계 영역 ---

procedure V(S) --> 현재상태는 S가 0임
    S := S+1   --> S를 1로 원위치시켜 해제하는 과정
end V
```
- P : S 값이 0보다 크면 1 감소시킨다. 0이면 1이 될 때까지 기다린다.
- V : S 값을 1 증가시킨다.

<br/>

## 뮤텍스 (Mutex)

### 뮤텍스란?

임계 구역을 가진 스레드들의 실행시간이 서로 겹치지 않고 각각 단독으로 실행되게 하는 기술로, 상호배제 (**Mut**ual **Ex**clusion)의 약자이다.

접근을 조율하기 위해 lock과 unlock을 사용한다.

- lock : 현재 임계영역에 들어갈 권한을 얻어온다. (만약 다른 프로세스/스레드가 임계 구역 수행 중이면 종료할 때까지 대기한다.)
- unlock : 현재 임계영역을 모두 사용했음을 알린다. (대기 중인 다른 프로세스/스레드가 임계영역에 진입할 수 있다.)

<br/>

### 1. 데커(Dekker) 알고리즘

flag와 turn 변수를 통해 임계 구역에 들어갈 프로세스/스레드를 결정하는 방식

- flag : 프로세스 중 누가 임계영역에 진입할 것인지 나타내는 변수
- turn : 누가 임계구역에 들어갈 차례인지 나타내는 변수

```java
while(true) {
    flag[i] = true; // 프로세스 i가 임계 영역 진입 시도
    while(flag[j]) { // 프로세스 j가 현재 임계 영역에 있는지 확인
        if(turn == j) { // j가 임계 영역 사용 중이면
            flag[i] = false; // 프로세스 i 진입 취소
            while(turn == j); // turn이 j에서 변경될 때까지 대기
            flag[i] = true; // j turn이 끝나면 다시 진입 시도
        }
    }
}

// ------- 임계 영역 ---------

turn = j; // 임계 영역 사용 끝나면 turn을 넘김
flag[i] = false; // flag 값을 false로 바꿔 임계 영역 사용 완료를 알림
```

<br/>

### 2. 피터슨(Peterson) 알고리즘

데커의 알고리즘과 유사하지만 상대방에게 진입 기회를 양보한다는 차이가 있고, 구현이 더 간단하다.

```java
while(true) {
    flag[i] = true; // 프로세스 i가 임계 영역 진입 시도
    turn = j; // 다른 프로세스에게 진입 기회 양보
    while(flag[j] && turn == j) { // 다른 프로세스가 진입 시도하면 대기
    }
}

// ------- 임계 영역 ---------

flag[i] = false; // flag 값을 false로 바꿔 임계 영역 사용 완료를 알림
```
<br/>

### 3. 베이커리(Bakery) 알고리즘

프로세스 n개의 상호배제 문제를 해결한 알고리즘. (여러 프로세스/스레드에 대한 처리 가능)

가장 작은 수의 번호표를 가지고 있는 프로세스가 임계영역에 진입한다.

```java
while(true) {
    
    isReady[i] = true; // 번호표 받을 준비
    number[i] = max(number[0~n-1]) + 1; // 현재 실행 중인 프로세스 중에 가장 큰 번호 배정 
    isReady[i] = false; // 번호표 수령 완료
    
    for(j = 0; j < n; j++) { // 모든 프로세스 번호표 비교
        while(isReady[j]); // 비교 프로세스가 번호표 받을 때까지 대기
        while(number[j] && number[j] < number[i] && j < i);
        
        // 프로세스 j가 번호표 가지고 있어야 함
        // 프로세스 j의 번호표 < 프로세스 i의 번호표
    }
}

// ------- 임계 영역 ---------

number[i] = 0; // 임계 영역 사용 종료
```
<br/><br/>

## 🔖 참고
[세마포어(Semaphore) & 뮤텍스(Mutex)](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Semaphore%20%26%20Mutex.md)
