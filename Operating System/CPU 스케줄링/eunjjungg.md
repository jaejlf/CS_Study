# 1. CPU 스케줄링

> 작업을 처리하기 위해 프로세스들에게 CPU를 할당하기 위한 정책을 계획하는 것<br/>
CPU 스케줄링 대상 프로세스는 Ready Queue의 프로세스로 스케줄링 정책에 따라 Queue에 정렬을 한 후 앞에 있는 프로세스부터 CPU를 할당함
> 

![image](https://user-images.githubusercontent.com/100047095/188310091-49e3728a-725c-4313-b5bc-5912217c04aa.png)

출처 : [https://steady-coding.tistory.com/509](https://steady-coding.tistory.com/509)

<br/>

**목적**

- CPU를 효율적으로 사용하기 위해 프로세스들을 잘 배정해야 함

<br/>

**목표, 스케줄링 Criteria**

- CPU Utilization : CPU가 쉬지 않아야 함
- Throughput : 단위 시간 당 처리량
- Turnaround Time : 수행을 요청한 후 작업이 끝날 때까지 걸린 시간
- Waiting Time : 수행을 요청한 후 작업이 시작될 때까지 걸린 시간 (Running 후 Ready Queue에 들어간 시간)
- Response Time : 수행을 요청한 후 응답이 올 때까지의 시간

<br/>

**시스템에 따른 목표**

- Batch System : 한 번에 하나의 프로그램만 수행 가능한 배치 시스템은 가능한 한 많은 일 수행이 목표
    - throughput
    - CPU Utilization
- Interactive System : 사용자가 컴퓨터 앞에서 대화형으로 동작하는 시스템
    - Response Time
    - Waiting Time
    - Proportionality : 사용자가 요구하는 바를 이루는가
- Real-time System : 시간 제약 조건이 걸려있는 시스템
    - Meetting Deadlines
    - Predictability

<br/><br/>

# 2. preemptive vs non-preemptive

- preemptive, 선점
    - OS가 CPU의 사용권을 선점할 수 있는 경우 강제로 회수
    - 장점
        - 높은 우선순위를 가진 프로세스를 빠르게 처리하는 시스템에 유용
        - 빠른 응답을 요구하는 시분할 시스템에 유용
    - 높은 우선 순위인 프로세스들만 들어오면 오버헤드 발생
- non-preemptive, 비선점
    - 프로세스 종료 또는 입출력 이벤트가 있을 때까지 실행을 보장
    - 장점
        - 모든 프로세스들에게 공정
        - 응답 시간을 예측할 수 있음
    - 단점
        - 짧은 작업을 수행하는 프로세스더라도 오래 대기할 수 있음

<br/><br/>

# 3. CPU 스케줄링 알고리즘

- **FCFS, First Come First Served**
    - 비선점 방식
    - 큐에 도착한 순서로 CPU 할당
    - CPU burst가 완료될 때까지 CPU를 반환하지 않음
    - 할당되었던 CPU가 반환될 때만 스케줄링이 이루어짐
    - 장점
        - 개발이 용이
        - 공평성 유지
        - 기아 문제가 발생하지 않음
    - 단점
        - 소요 시간이 긴 프로세스가 먼저 도착하는 경우 효율성이 낮아짐
        - 실행시간이 짧더라도 뒤늦에 도착한 경우 대기 시간이 길어짐

- **SJF, Shortest Job First**
    - 비선점 방식
    - FCFS 보완 알고리즘
    - 수행 시간이 가장 짧다고 판단되는 작업을 우선 수행
    - 짧은 작업 수행시에는 유리
    - 기아 문제 발생 가능 : 사용 시간이 긴 프로세스는 영원히 CPU를 할당받지 못함

- Priority 스케줄링
    - 선점, 비선점 모두 가능함
    - 프로세스에 우선 순위를 부여하여 우선 순위가 높은 순서대로 작업을 처리
    - 기아 문제 발생 가능
    - Indefinite Blocking 발생 가능 : 실행 준비가 되어 있으나 CPU를 사용하지 못하는 프로세스가 CPU를 무한정 기다리는 상태

- **SRTF, Shortest Remaining Time First**
    - 선점 방식
    - 현재 수행 중 프로세스의 남은 burst time보다 더 짧은 CPU burst time을 가진 프로세스가 들어올 경우 CPU를 강제로 회수
    - 새로운 프로세스가 들어올 때마다 스케줄링을 다시함
    - CPU 사용 시간을 예측할 수 없음
    - 기아 문제 발생 가능

- **Round Robin**
    - 선점 방식
    - 현대적인 스케줄링 방식
    - FCFS에 의해 프로세스를 받아 각 프로세스에 동일한 시간의 Time Quantum만큼 CPU 할당
    - 할당 시간이 끝나면 Ready Queue의 제일 뒤에 삽입됨
    - CPU 사용 시간이 랜덤한 프로세스들이 많은 경우 유용함
    - 장점
        - Response Time이 빨라짐
        - 프로세스가 기다리는 시간이 CPU를 사용할 만큼 증가하는 fair 스케줄링 방식
    - Time Quantum이 크면 FCFS와 다를게 없어지고 작으면 Context Switching이 너무 빈번하게 일어나서 오버헤드 발생

- **Multilevel-Queue, 다단계 큐**
    - 작업들을 여러 종류의 그룹으로 나누어 여러 개의 Queue를 사용
    - 우선순위가 낮은 큐들이 실행 되지 못하는 것을 방지하기 위해 큐마다 다른 Time Quantum을 설정

- **Multilevel-Feedback-Queue, 다단계 피드백 큐**
    - 다단계 큐에서 자신에게 할당된 Time Quantum을 다 사용한 프로세스는 밑으로 내려가고 Time Quantum을 다 채우지 못한 프로세스는 그 큐에 그대로 존재
    - 짧은 작업에 유리함
    - 처리 시간이 짧은 프로세스를 먼저 처리함
