# 💡 Blocking,Non-blocking & Synchronous,Asynchronous	

Blocking/Non-blocking 과 Sync/Async 은 흔히 같은 개념이라고 착각하기 쉽다.

즉, Blocking이라고 해서 반드시 Sync이거나, Non-blocking이라고 해서 반드시 Async인 것은 아니다.

각각의 의미와 차이를 살펴보자.


<br/>

## Blocking & Non-blocking

Blocking/Non-blocking 은 `제어권` 의 관점으로 접근해야 한다.

다시 말해, blocking과 non-blocking은 `호출된 함수` 가 `호출한 함수` 에게 제어권을 건네주는 여부에 따라 결정된다.

### Blocking &rarr; 기다림

호출된 함수가 자신이 할 일을 다 마칠 때까지 호출한 함수에게 **제어권을 넘겨주지 않는 것**을 말한다.

따라서, 호출한 함수는 다른 작업을 수행하지 못 하고, 제어권이 돌아오기(호출된 함수가 종료될 때까지)를 **기다려야 한다.**

### Non-blocking &rarr; 다른 일 수행

호출된 함수가 자신의 할 일을 다 마치지 않았어도 호출한 함수에게 **바로 제어권을 넘겨주는 것**을 말한다.

따라서, 호출한 함수는 호출된 함수의 작업 처리 여부와 상관 없이 **다른 작업들을 수행할 수 있다.**

<br/>

## Synchronous & Asynchronous

Synchronous/Asynchronous 는 `시간`, `동시성` 의 관점으로 접근해야 한다.


### Synchronous (동기) &rarr; 결과 바로 처리

**끝나는 동시에 시작하는 것**을 말한다.

즉, 호출된 함수가 결과를 리턴하면 호출한 함수는 바로 그 결과에 집중하여 처리한다.

### Asynchronous (비동기) &rarr; 결과 바로 처리하지 않음

시작과 종료가 일치하지 않으며, **끝나는 동시에 시작하지 않는 것**을 말한다.

즉, 호출된 함수가 결과를 리턴하면 호출한 함수는 그 결과를 바로 처리하지 않아도 된다.


<br/>

## 조합

이제 4가지 조합을 알아보자!

![](https://velog.velcdn.com/images/wisdom-one/post/a9f2b953-897a-4d8b-9bff-fe2fa6031994/image.png)

2가지 개념을 조합하면 헷갈릴 수 있는데 다음과 같이 생각하면 이해가 편하다.

- blocking : 끝날 때까지 기다림
- non-blocking : 다른 일 수행
- sync : 반환 결과 바로 처리
- async : 반환 결과 바로 처리하지 않음

<br/>

### 1) Blocking/Sync

"기다림 + 결과 바로 처리"

호출한 함수는 호출된 함수가 종료될 때까지 (다른 일은 하지 못하고) 기다리고, 호출된 함수로부터 결과를 받으면 바로 처리한다.

ex. 자바에서 입력 요청을 할 때

<br/>

### 2) Non-Blocking/Sync

"다른 일 수행 + 결과 바로 처리"

호출한 함수는 호출된 함수 실행 중에 다른 일을 수행하다가, 호출된 함수가 종료된 것을 확인하면 그 결과를 바로 처리한다.

<br/>

### 3) Blocking/Async

"기다림 + 결과 바로 처리하지 않음"

호출한 함수는 호출된 함수가 종료될 때까지 (다른 일은 하지 못하고) 기다리고, 호출된 함수로부터 결과를 받으면 바로 처리하지 않아도 된다.

&rarr; 호출된 함수의 결과를 바로 처리하지 않아도 되는데도 다른 일은 못 하고 기다리는 이상한 상황이다..

<br/>

### 4) Non-Blocking/Async

"다른 일 수행 + 결과 바로 처리하지 않음"

호출한 함수는 호출된 함수 실행 중에 다른 일을 수행할 수 있고, 호출된 함수로부터 결과를 받으면 바로 처리하지 않아도 된다.

ex. 자바스크립트 API 요청 with 콜백

<br/><br/>

## 🔖 참고
- [gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/%5BNetwork%5D%20Blocking%2CNon-blocking%20%26%20Synchronous%2CAsynchronous.md)
- [블로그](https://programming119.tistory.com/238)
- [블로그](https://studyandwrite.tistory.com/486)
