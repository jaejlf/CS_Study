# 프로세스 vs 스레드

## A. 프로세스와 스레드란?

<img src="https://camo.githubusercontent.com/3dc4ad61f03160c310a855a4bd68a9f2a2c9a4c7/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393938383931343635433637433330363036">

<br>

**프로세스**는 메모리에 적재되고 CPU 자원을 할당받아 프로그램이 실행되는 상태를 말한다.

**스레드**는 어떤 프로그램 내에서, 특히 스레드 내에서 실행되는 흐름의 단위를 말한다.

일반적으로 하나의 애플리케이션(프로그램)은 하나 이상의 프로세스를 가지고, **하나의 프로세스는 반드시 하나 이상의 스레드**를 갖는다.

<br>

> +) 프로그램이란?
> <br>
> 파일이 저장 장치에 저장되어 있지만, 메모리에는 올라가 있지 않은 정적인 상태

프로그램은 아직 실행되지 않고 가만히 있는 상태, 프로그램을 실행하여 메모리에 적재된 동적인 상태가 프로세스

<br>

## B. 프로세스의 구조와 멀티태스킹

멀티태스킹은 OS를 통해 CPU가 작업한느 데 **필요한 자원(시간)을 프로세스 또는 스레드 간 나누는 행위**를 말한다.

→ 멀티태스킹을 통해 여러 응용 프로그램을 동시에 열고 작업할 수 있다

<br>

### 프로세스 구조

<br>

<img src="https://static.javatpoint.com/difference/images/process-vs-thread2.png">

- 스택 영역(`stack`): 지역 변수를 저장한다
- 코드 영역(`code`, text): 프로그래머가 작성한 프로그램이 코드 영역에 저장된다.
- 데이터 영역(`data`): 코드가 실행되면서 사용한 변수나 파일들의 데이터
- 힙 영역(`heap`): 동적으로 할당데는 데이터가 저장된다.

<br>

코드 영역과 데이터 영역은 선언할 때 그 크기가 결정되는 정적 영역

스택 영역과 힙 영역은 프로세스가 실행되는 동안 크기가 가변적인 동적 영역

원칙적으로 **서로 다른 프로세스 간 메모리 공간 접근은 허용되지 않는다.**

<br>

## C. 스레드

> 스레드: 어떠한 프로그램 내에서, 특히 프로세스 내에서 실행되는 흐름의 단위

<br>

일반적으로 하나의 애플리케이션(프로그램)은 하나 이상의 프로세스를 가지고 있고, **하나의 프로세스는 하나 이상의 스레드**를 갖는다.
<br>

→ 프로세스를 생성하면 기본적으로 하나의 (메인) 스레드가 생성된다

<br>

### 스레드 구조

<br>

스레드는 프로세스 내에서 **Stack만 따로 할당**받고, Code, Data, Heap 영역은 공유한다.

스레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, **같은 프로세스 안에 있는 여러 스레드들은 힙 공간을 공유**한다.

따라서 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드도 변경 결과를 즉시 볼 수 있다.

> 프로세스 vs 스레드: 프로세스는 자원을 공유 ❌, 스레드는 자원 공유

<br>

## D. 멀티 프로세스와 멀티 스레드

<br>

<img src="https://images.velog.io/images/sehrltjr/post/eb4dec8d-0bcd-49ef-9dbf-f18a1bfb3096/image.png">

<br>

- 멀티 프로세스: 두 개 이상의 다수의 프로세서(CPU)가 협력적으로 하나 이상의 작업(Task)를 동시에 처리하는 것 (병렬 처리)

- 멀티 스레드: 하나의 애플리케이션을 여러 개의 스레드로 구성하여 하나의 스레드가 하나의 작업을 처리하도록 하는 것

<br>

### 멀티 프로세스

- 장점
  - **안정성**이 좋다. 독립된 구조이기 때문에 하나의 자식 프로세스에 문제가 발생해도 다른 자식 프로세스에는 영향을 미치지 않는다.
  - **구현이 비교적 간단**하다. 각 프로세스들이 독립적으로 동작하며 자원이 서로 다르게 할당된다.
- 단점
  - 프로그램 간 통신을 위해서는 IPC를 통해야 한다.
  - 메모리 사용량이 많다.
  - 독립된 메모리 영역이기 때문에 작업량이 많을수록(`Context Switching`이 자주 일어나서 주소 공간의 공유가 잦을 경우) 오버헤드가 발생하여 성능 저하 발생

<br>

#### Context Switching

- CPU는 한 번에 한 가지 프로세스만 실행 가능하다.
- 따라서 CPU에서 여러 프로세스를 돌아가면서 작업을 처리하는 것을 **Context Switching** 이라고 한다.
- 동작 중인 프로세스가 대기하면서 해당 프로세스의 상태(Context)를 보관하고, 대기하고 있던 다음 순서의 프로세스가 동작하면서 이전에 보관했던 프로세스의 상태를 복구하는 작업

<br>

### 멀티 스레드

하나의 프로세스에서 여러 스레드로 작업을 공유하며 작업을 수행하는 것

- 장점
  - 응답성이 좋다. 프로그램의 일부분(자식 스레드)이 오류 또는 긴 작업으로 중단되어도 프로그램은 계속 수행된다
  - 자원 공유가 쉽다. 스레드들은 부모 프로세스의 자원과 메모리를 공유
  - 멀티프로세서 구조에서 각각의 스레드가 다른 프로세서에서 병렬로 수행될 수 있다.
- 단점
  - 구현 및 테스트, 디버깅이 어렵다
  - 너무 많은 스레드 사용은 오버헤드를 발생시킨다
  - 동기하 및 교착 상태가 발생하지 않도록 주의해야 한다.
  - 자식 스레드 중 하나에 문제가 생긴 경우 전체 프로세스에 영향을 줄 수 있다.

<br>

#### 멀티 프로세스 vs 멀티 스레드

| 종류              | 장점                                                                                              | 단점                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **멀티 프로세스** | 하나의 프로세스가 죽어도 다른 프로세스에는 영향 X                                                 | 각각 독립된 메모리 영역 가지고 있어 작업량이 많을 수록 오버헤드 발생, Context Switching으로 인한 성능 저하 유발 |
| **멀티 스레드**   | 프로세스의 응답시간 단축 & 시스템의 처리율 향상<br> 코드 영역과 데이터 영역 공유해 자원 소모 적다 | 프로그램 디버깅이 어렵고 하나의 스레드에 문제 생기면 전체 프로세스에 영향                                       |

##### 멀티 스레드가 멀티 프로세스에 비해 가지는 장점

- **자원의 효율성 증대**

프로세스 생성하여 **자원을 할당하는 비율이 작고**, 스레드는 프로세스 내의 메모리를 공유하기 때문에 독립적인 프로세스와 달리 **스레드 간 데이터를 주고받는 것이 간단**해지고 **시스템 자원 소모가 줄어든다.**

- **응답 시간 단축 및 처리 비용 감소**

프로세스 간 IPC를 통해 통신하는 것은 상대적으로 비용 크다.
그러나 프로세스는 프로세스의 메모리 영역을 공유하므로 **스레드 간 통신 비용**이 적게 든다.

프로세스 간 Context Switching은 느린 반면 스레드 간 Context Switching은 Stack 영역만 처리하면 되므로 상대적으로 빠르다.

#### 멀티 스레드가 멀티 프로세스에 비해 가지는 단점

- **멀티 스레드의 안전성 문제**

여러 개의 스레드가 동일한 데이터 공간(Critical Section)을 공유하며 이들을 수정하기 때문에 발생하는 문제

멀티 프로세스의 프로그램은 문제가 생기면 해당 프로그램을 중단 혹은 종료 후 다시 시작하면 된다.

그러나 멀티 스레드 방식 프로그램에서는 하나의 스레드가 자신이 사용하는 데이터 공간을 망가뜨리면, **해당 데이터 공간을 사용하는 모든 스레드를 망가뜨릴** 수 있다.

## 참고자료

🔗 https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%E2%9A%94%EF%B8%8F-%EC%93%B0%EB%A0%88%EB%93%9C-%EC%B0%A8%EC%9D%B4

🔗 https://livenow14.tistory.com/67
