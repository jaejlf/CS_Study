# 1. 프로세스

> **프로그램** : 파일이 저장 장치에 저장되어 있지만 메모리에 올라가 있지 않은 정적인 상태 <br/>
**프로세스** : 운영체제로부터 자원을 할당받은 작업의 단위 <br/>
**메모리에 올라가 있지 않은** : 아직 운영체제가 프로그램에게 독립적인 메모리 공간을 할당해주지 않은 상태, 모든 프로그램은 운영체제가 실행되기 위한 메모리 공간을 할당해줘야 실행할 수 있음 <br/>
**정적인 상태** : 아직 실행되지 않은 상태 <br/>
**할당 받는 자원의 예** : CPU 시간 / 운영되기 위한 주소 공간 / Code, Data, Stack, Heap의 구조로 되어 있는 독립된 메모리 영역 <br/>
**Code** : 코드 자체를 구성하는 메모리 영역 <br/>
**Data** : 전역 변수, 정적 변수, 배열 등 <br/>
**Heap** : 동적 할당 시 사용 <br/>
**Stack** : 지역 변수, 매개 변수, 리턴 값 (임시 메모리 영역)
> 

✅ 코드 덩어리인 **프로그램** → 실행을 누르면 → 파일이 컴퓨터 메모리에 올라가게 됨 : 동적인 상태가 되고 이 상태의 프로그램을 **프로세스**라고 함 <br/><br/>

# 2. 스레드

> **스레드** : 프로세스가 할당받은 자원을 이용하는 실행 흐름의 단위
> 

이제는 프로그램 하나가 단순히 한 가지 작업만을 하는 경우는 없음 <br/>
→ 프로세스보다 더 작은 실행 단위인 스레드의 기준으로 작업을 수행함 <br/>

|  | 프로세스 | 스레드 |
| --- | --- | --- |
| 메모리 공유 | X | O |

스레드는 프로세스의 자원을 공유하면서 프로세스의 실행 흐름의 일부가 됨 <br/><br/>

# 3. 프로세스와 스레드의 작동 방식

- 프로세스가 메모리에 올라갈 때 운영체제로부터 독립된 메모리 형태를 Code, Data, Stack, Heap의 형식으로 할당해줌 → 프로세스끼리는 서로의 자료나 변수에 접근할 수 없음
    
    ![image](https://user-images.githubusercontent.com/100047095/182940916-39ced688-2c2d-4a63-9914-d29ed94cff0f.png)
    
    출처 : [https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html](https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html) <br/><br/>
    

- 반면 스레드는 메모리들을 서로 공유할 수 있음
엄밀히 말하자면, 프로세스가 할당 받은 메모리 영역 내에서 Stack 형식으로 할당된 메모리 영역은 따로 할당 받고, 나머지 Code, Data, Heap 형식으로 할당된 메모리 영역은 공유 <br/>
✅ 각각의 스레드는 별도의 스택을 가지고 있지만 힙 메모리는 서로 읽고 쓰기 O
    
    ![image](https://user-images.githubusercontent.com/100047095/182940938-c73ff868-5af8-480c-9482-c5ba3be110c4.png)
    
    출처 : [https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html](https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html) <br/><br/>
    

- 만약 한 프로세스를 실행하다가 오류가 발생해 프로세스가 강제 종료 된다면 공유 파일을 손상시키는 경우를 제외하면 다른 프로세스에 아무런 영향을 주지 않음 <br/>

- 반면 스레드의 경우에는 Code, Data, Heap을 공유하고 있기 때문에 하나의 스레드에서 오류가 나면 같은 프로세스의 나머지 스레드들 모두 강제 종료됨 <br/>

- 운영체제 관점에서의 최소 작업 단위는 프로세스
 CPU 관점에서의 최소 작업 단위는 스레드 <br/><br/>

# 4. 멀티프로세싱, 멀티스레드

> **멀티프로세싱** : 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리하도록 하는 것 <br/>
**멀티스레드** : 하나의 프로세스가 여러 작업을 여러 스레드를 통해 동시에 처리하는 것<br/>
**Context-Switching** : CPU에서 여러 프로세스를 돌아가면서 작업을 처리하는 것, 동작 중인 프로세스가 대기를 하면서 해당 프로세스의 상태(Context)를 보관하고 대기하고 있던 다음 순서의 프로세스가 동작하면서 이전에 보관했던 프로세스의 상태를 복구하는 작업
> 



### a. 멀티프로세스의 장점

여러 개의 자식 프로세스 중 하나에 문제가 발생하면 그 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않음 <br/><br/>

### b. 멀티프로세스의 단점

Context-Switching 과정에서 캐쉬 메모리 초기화 등 무거운 작업이 진행되고 많은 시간이 소모되는 등의 오버헤드가 발생하게 됨 

프로세스끼리 공유하는 데이터가 없기 때문에 Context-Swtiching이 발생하면 기존 데이터를 모두 리셋하고 다시 캐시 정보를 불러와야 되기 때문 

프로세스끼리 통신하는 방법이 존재하기는 하는데 (IPC, Inter-Process Comunication) 어려움! <br/><br/>

### c. 프로세스끼리 통신?

프로세스가 다른 프로세스의 정보에 접근하는 것이 가능은 함

그러나 프로세스간 정보를 교체하는 방법은 CPU 레지스터 교체 뿐 아니라 RAM과 CPU 사이의 캐시 메모리까지 초기화되기 때문에 자원 부담이 큼 

방식은 아래의 세 가지가 있음

- IPC (Inter-Process Communication)
- LPC (Local-Process Communication)
- 별도로 공유 메모리를 만들어 정보를 주고받도록 설정 <br/><br/>

### d. 멀티스레드의 장점

Context-Switching할 때 공유하고 있는 메모리만큼의 메모리 자원을 아낄 수 있음 (반면 프로세스간의 Context-Switching은 많은 자원 손실이 발생) → **시스템 자원의 효율성 증대** 

스레드는 프로세스 내의 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 통신의 부담이 적어서 응답 시간이 빠름 → **시스템 처리량 증가로 이어짐** <br/><br/>

### e. 멀티스레드의 단점

스레드 하나가 프로세스 내 자원을 망쳐버린다면 모든 프로세스가 종료됨

단일 프로세스의 경우에는 효과를 기대하기 어려움

자원을 공유하기 때문에 필연적으로 동기화 문제가 발생함 <br/><br/>

### f. 동기화 문제, Synchronization Issue?

멀티 스레드를 사용하면 각각의 스레드 중 어떤 것이 어떤 순서로 실행될지 그 순서를 알 수 없음

ex) A 스레드가 c 자원을 사용하여 작업 → B 스레드로 제어권이 넘어감 → B 스레드가 c 자원을 수정 → A 스레드로 제어권이 넘어감 → A 스레드가 c 자원에 접근하지 못하거나 바뀐 자원에 접근하게 됨
