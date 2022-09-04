# IPC(Inter-Process Communication)

> 프로세스 사이에 서로 데이터를 주고받는 행위 또는 그에 대한 방법이나 경로

<br>

- 프로세스는 독립적으로 실행되기 때문에 다른 프로세스에 영향을 받지 않는다.
- 독립적인 구조를 가진 **프로세스 간 통신**을 위해 IPC가 사용된다.
- 프로세스는 커널이 제공하는 IPC를 이용하여 프로세스 간 통신이 가능하다.

<br>

+) 스레드의 경우 프로세스 안에서 자원을 공유하므로 영향을 받는다.

## A. IPC의 종류

- 익명 PIPE
    - PIPE: 두개의 프로세스 연결 시 하나의 프로세스는 데이터 쓰기만 가능, 다른 프로세스는 데이터 읽기만 가능<br>한쪽 방향으로만 통신이 가능한 반이중 통신!
    - 양쪽 모두 송/수신하려면 2개의 파이프 필요
    - 통신할 프로세스 명확히 알 수 있는(ex. 부모-자식 간 프로세스 통신), 상호 관련 **있는** 프로세스 간 통신에 사용
    - 장점: 매우 간단히 사용 가능, 단순한 데이터 흐름 시 유용
    - 단점: 전이중 통신 위해 2개 만들 시 구현 복잡해짐
- Named PIPE(FIFO)
    - 장치 파일을 통해 상호 관련 **없는** 프로세스 간 통신에 사용
    - 익명 파이프의 확장된 상태
    - 부모 프로세스와 무관한 다른 프로세스도 통신 가능(통신 위해 이름없는 파일 사용)
    - 익명 PIPE처럼 동시에 읽기/쓰기 불가능
- Message Queue
    - 입출력 방식은 Named 파이프와 동일
    - PIPE: 데이터 흐름, Queue: **메모리 공간**
    - 사용할 데이터에 번호를 붙이면서 여러 프로세스가 동시에 데이터 다루기 가능
- 공유 메모리
    - 파이프, 메세지 큐: 통신을 위한 설비
    - 공유 메모리: 데이터 자체!
    - 프로세스 간 메모리 영역 공유해서 사용할 수 있도록 허락
    - 중개자 없이 곧바로 메모리에 접근 가능해 IPC 중 가장 빠르다
- 메모리 맵
    - 공유 메모리처럼 메모리 공유
    - 열린 파일을 메모리에 맵핑시켜 공유
    - 파일로 대용량 데이터 공유해야 할 시 사용
- 소켓
    - 네트워크 소켓 통신을 통해 데이터 공유
    - 클라이언트-서버가 소켓 통해 통신
    - 원격에서 프로세스 간 데이터 공유 시 사용

<br>

IPC 통신에서 프로세스 간 데이터 동기화/보호 시 세마포어와 뮤텍스 사용<br>
-> 세마포어와 뮤텍스의 역할: 한 번에 하나의 프로세스만 접근할 수 있게 해준다.


    

