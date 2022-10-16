# Blocking, Non-Blocking & Synchronous , Asynchronous

## 📌 A. 동기와 비동기(Synchronous and Asynchronous)

<br/>

### 동기

> 현재 작업의 응답과 다음 작업 요청의 타이밍을 맞추는 것

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fwonhee010%2Fpost%2Fdd6c1aab-eeec-453d-b43c-5f3dc9db9b4c%2Fimage.png" alt="text" width="485" />
</p>

<br/>

- 작업이 어떤 순서를 가지고 진행하는 것
- `Thread1`이 작업을 시작하고, `Task1`이 종료될 때까지 기다렸다 `Task2`를 시작
- 작업 요청 시 요청의 **결과값(return)** 을 직접 받는 것
- **호출한 함수가 작업 완료를 신경쓴다**
- 상위 프로세스가 하위 프로세스에게 작업을 지시할 때 작업의 종료 시점을 알고 있어야 한다.

<br>

### 비동기

> 현재 작업의 응답과 자음 작업의 응답이 일치하지 않아도 된다.

<br/>

<p align="center">
  <img src="https://evan-moon.github.io/static/ec1da404358cadaa685c34ecb3f1fb8a/eea4a/async.jpg" alt="asynchronous" width="485" />
</p>

<br/>

- 작업의 종료 시점을 신경 쓰는 동기 방식과 다르게, 상위 프로세스는 작업을 지시한 후에는 하위 프로세스의 작업에 언제 종료되는지 신경쓰지 않는다.
- 상위 프로세스가 하위 프로세스의 작업 종료 여부를 신경쓰지 않기 때문에 작업의 종료가 순차적으로 이루어지는 것을 보장하지 않는다.

<br/>

### 동기와 비동기

> 호출되는 함수의 작업 완료 여부를 누가 신경쓰느냐가 관심사

<br/>

- 호출되는 함수에게 **callback**을 전달하여 호출되는 함수가 전달받은 callback을 실행하고, **호출된 함수는 작업 완료 여부를 신경쓰지 않는다.** 👉 비동기

- 호출하는 함수가 호출되는 함수의 작업 완료 후 return을 기다리거나
  호출되는 함수로부터 바로 return 받더라도 작업 완료 여부를 호출한 함수 스스로 확인하며 신경 쓴다 👉 동기

<br/>

## 📌 B. 블로킹과 논 블로킹

<br/>

### 블로킹

- 요청한 작업을 마칠 때까지 계속 대기
- 즉시 return한다.
- return 값을 받아야 끝난다.
- Thread 관점으로 본다면, 요청한 작업을 마칠 때까지 계속 대기하며 return 값을 받을 때까지 한 Thread를 계속 사용/대기 한다.

<br/>

### 논블로킹

- 요청한 작업을 즉시 마칠 수 없다면 즉시 return한다.
- 즉시 리턴하지 않는다. (일을 못하게 막는다.)
- Thread 관점으로 본다면, 하나의 Thread가 여러 개의 IO를 처리 가능하다.

<br/>

### 블로킹과 논 블로킹

> 이 그룹은 호출되는 함수가 바로 return하느냐 마느냐가 관심사

<br/>

- 호출된 함수가 바로 return해서 호출한 함수에게 제어권을 넘겨주고
  호출한 함수가 다른 일을 할 수 있는 기회를 줄 수 있다 👉 non-blocking

- 호출된 함수가 자신의 작업을 모두 마칠 때까지
  호출한 함수에게 제어권을 넘겨주지 않고 대기하게 만든다 👉 blocking

<br/>

## 📌 C. 블로킹과 논 블로킹, 동기와 비동기

<br/>

### blocking + Synchronous, non-blocking + Asynchronous

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fwonhee010%2Fpost%2F3f0ce3ff-b477-4399-a8ba-8a44aa6b0e6e%2FiSafBIF.png" alt="asynchronous" width="485" />
</p>

<br/>

#### blocking + Synchronous

<br/>

<p align="center">
  <img src="https://evan-moon.github.io/static/fe251be8bc28c901b166ea3f99eb1302/eea4a/sync-block.jpg" alt="asynchronous" width="485" />
</p>

- 가장 흔하게 접하는 동기 방식의 예 `동기 & 블로킹`
- 동기 방식이기 때문에 작업의 흐름이 순차적으로 진행디는 것 보장
- 블로킹 방식이기 떄문에 어떠한 작업이 진행 중일때는 다른 작업을 동시에 진행할 수 없읍
- 하나의 콜스택에 작업을 넣고 `Last In First Out`으로 진행됨

<br/>

결과가 처리되어 나올때까지 기다렸다가 return 값으로 결과를 전달한다.

<br/>

#### non-blocking + asynchronous

<br/>

- 비동기 방식이기 때문에 상위 프로세스는 하위 프로세스의 작업 완료 여부를 따로 신경쓰지 않는다.

- 논블로킹 방식이기 때문에 상위 프로세스는 하위 프로세스에게 일을 맡기고 자신의 작업을 계속 수행할 수도 있다.

<br/>

<p align="center">
  <img src="https://evan-moon.github.io/static/576918463dddd506e08ef5a97177dd7e/eea4a/async-non-block.jpg" alt="asynchronous" width="485" />
</p>

- 이 예제를 보면 `boss` 함수는 `employee` 함수에게 인형 눈알 100개를 붙히라고 지시한 후 자신은 바로 퇴근.
- 상위 프로세스인 `boss` 함수는 `employee` 함수의 작업이 언제 끝나는지는 관심이 없으며 작업의 완료 신호는 콜백으로 넘겨진 `눈알 결산 보고 작업`이 대신 받아서 처리하고 있다.

<br/>

- 장점: 여러 개의 방식을 동시에 처리할 수 있어 효율적
- 단점: 너무 복잡하게 얽힌 비동기 처리 때문에 개발자가 어플리케이션의 흐름을 읽기 어려워지는 등의 문제가 있을 수 있다

<br/>

#### non-blocking + synchronous

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fwonhee010%2Fpost%2F9f44f41f-e03c-45e0-90b0-1751e86aeb70%2Fa8xZ9No.png" alt="asynchronous" width="485" />
</p>

- 동기는 작업들이 순차적인 흐름을 지니고 있다는 것을 의미. 이 흐름만 지켜지면 된다.

<br/>

<p align="center">
  <img src="https://evan-moon.github.io/static/6395f57fdd8a1d9b8bdbb83621f2157c/eea4a/sync-non-block.jpg" alt="asynchronous" width="485" />
</p>

이 예제를 살펴보면

- boss 함수는 출근 후 하위 프로세스인 employee를 호출하여 눈알 붙이기 작업을 시키고 주기적으로 작업이 끝났는지 검사
- 분명히 동기적인 흐름을 가지고 진행하고 있지만 boss 함수 또한 중간중간 자신의 작업을 수행하고 있으므로 블록킹이 아니라 논블록킹 방식을 사용하고 있다
- boss 함수는 employee 함수의 작업이 끝나기 전까지는 절대 퇴근할 수 없다. 작업의 순서가 지켜지고 있는 것이다.

👉 동기 방식이라는 것은 작업의 순차적인 흐름만 지켜진다면 블록킹이든 논블록킹이든 아무 상관이 없다고 할 수 있다.

<br/>

#### blocking + Asynchronous

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fwonhee010%2Fpost%2Fbc20459f-02fe-431a-a1d0-8d5016a964f9%2FzKF0CgK.png" alt="asynchronous" width="485" />
</p>

- 일반적인 어플리케이션 레이어에서는 자주 사용되지 않고 Linux와 Unix 운영체제의 I/O 다중화 모델 정도의 저레벨에서 사용되고 있다

- 프로세스가 블로킹되어 유휴 상태에 빠지면 아무것도 처리할 수 없기 때문에, 언뜻 보면 여러 개의 작업을 동시에 처리할 수 있다는 비동기의 장점을 살리기 힘들어 보인다.<br/>
  👉 그러나 블로킹 + 비동기 방식이 등장하게 된 이유는 다음과 같다

<br/>

<블로킹 + 비동기 방식의 등장 이유>

1. 동기 & 블록킹 I/O의 경우 직관적이나, 여러 개의 I/O를 동시에 처리할 수 없다.
2. 논블록킹 I/O는 프로세스들의 작업을 컨트롤하는 것이 까다롭다.
3. 그렇다고 동기 & 블록킹 I/O와 멀티 프로세싱이나 쓰레딩을 결합해서 쓰면 자원 문제도 있고 프로세스/쓰레드 간 통신이나 동기화가 어렵다.

<br/>

그래서 등장한 개념이 프로세스를 블로킹하고 비동기로 여러 개의 I/O를 다중화해서 받는 것.
직관적인 코드 흐름을 유지하면서도 작업을 동시에 처리하겠다는 것이다.

<Br/>

<p align="center">
  <img src="https://evan-moon.github.io/0855a1508418e6ca6cb4b933f2dc3e61/async-block.gif" alt="asynchronous" width="485" />
</p>

- 비동기 & 블록 방식의 대표적인 예인 select 함수가 작동하는 방식

  - 일정 시간동안 프로세스를 멈춰놓고 자신이 감시하고 있는 파일들에서 I/O가 발생하는지를 감시
  - 일정 시간이 지나면 함수가 종료되며 그동안 감시했던 파일들의 I/O 결과를 반환하고 프로세스의 블록킹이 풀린다

- 장점
  - 블록킹 방식으로 진행되기 때문에 개발자에게도 직관적으로 다가오고, 비동기 방식이기 때문에 여러 개의 I/O를 동시에 감시하며 처리할 수 있다.
- 단점
  - 성능이 그리 좋은 편은 아니므로 IBM에서는 높은 성능이 필요한 애플리케이션에서는 권고하지 않음

<br/>

## 📌 D. 참고자료

🔗 [동기(Synchronous)는 정확히 무엇을 의미하는걸까?](https://evan-moon.github.io/2019/09/19/sync-async-blocking-non-blocking/)

🔗 [동기 vs 비동기 (feat. blocking vs non-blocking)](https://velog.io/@wonhee010/%EB%8F%99%EA%B8%B0vs%EB%B9%84%EB%8F%99%EA%B8%B0-feat.-blocking-vs-non-blocking)
