# 💡 CPU Scheduling

## 1. 목적 및 기준

### 목적
- CPU를 할당받을 프로세스를 잘 골라 실행시켜줌으로써 시스템의 전체적인 성능을 높이는 것을 목적으로 한다.
- `Batch System (일괄처리 시스템)` : 높은 처리량 (throughput)
- `Interactive System (대화형 시스템)` : 빠른 응답 시간 (response time)
- `Realtime System (실시간 시스템)` : 기한 (deadline) 맞추기

### 성능 지표
- `응답 시간 (Response Time)` : 프로세스의 요청에 대해 시스템이 최초로 출력을 내주기 시작할 때까지 걸린 시간
- `처리량 (hroughput)` : 단위 시간에 완료된 프로세스의 개수

<br/>

## 2. 스케줄링 시점

<img width="50%" src="https://velog.velcdn.com/images/wisdom-one/post/fc70536e-d646-4a82-96a9-4c2f500398f8/image.png"/>

스케줄링이 언제 사용되는지 정리하면 다음과 같다.

1. 프로세스 실행 &rarr; 대기 (ex. 입출력 요청)
2. 프로세스 실행 &rarr; 준비 (ex. 시간 종료와 같은 인터럽트 발생)
3. 프로세스 대기 &rarr; 준비 (ex. 입출력 종료)
4. 프로세스 종료


<br/>

## 3. 선점 / 비선점 스케줄링

선점(Preemptive) 스케줄링
- CPU를 할당받아 실행 중인 프로세스로부터 CPU를 선점하여 다른 프로세스에게 할당할 수 있는 방식

비선점(Non Preemptive) 스케줄링
- 한 프로세스가 CPU를 할당받았을 때 CPU를 스스로 반납할 때까지 계속 사용하도록 허용하는 방식
- 위의 스케줄링 시점 중에서 `실행 → 대기`, `종료` 에만 스케줄링이 가능하다.

<br/>

## 4. 스케줄링 기법

### 비선점(Non Preemptive) 스케줄링
#### 1) FCFS (First Come First Served)
- 프로세스가 대기 큐에 `도착 순서`에 따라 CPU를 할당한다.
- 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어진다.
- FIFO 알고리즘


#### 2) SJF (Shortest Job First)
- 프로세스가 도착하는 시점에 따라, 그 당시 가장 `짧은 수행 시간`을 갖는 프로세스에게 CPU를 할당한다.
- 평균 대기 시간 최소화
- `기아 현상`이 발생할 수 있다.


#### 3) HRN (High Response Ratio Next)
- 대기 시간과 실행 시간을 모두 고려하여 우선순위를 계산하고, 가장 우선순위가 높은 프로세스에게 CPU를 할당한다.
- 우선순위 = $\frac {대기 시간 + 수행 시간} {수행 시간}$
- SJF의 약점인 기아 현상을 보완하는 기법이다.


<br/>

### 선점(Preemptive) 스케줄링

#### 1) Round Robin
- FCFS 스케줄링을 기반으로 CPU를 할당하되, 각 프로세스는 CPU 시간 크기 즉, 시간 할당량(Time Quantum)만큼만 CPU를 할당받는다.
- 프로세스가 할당된 시간 내에 완료하지 못하면, 큐의 맨 마지막으로 보내지고 CPU는 대기 중인 다음 프로세스에게 넘어간다.
- 할당 시간(Time Quantum)이 크면 FCFS와 같게 되고, 작으면 문맥 교환 (Context Switching) 잦아져서 오버헤드가 증가한다.
- 대화식 시스템이나 시분할 시스템에 적합한 방식이다.

#### 2) SRT (Shortest Remaining Time First)
- 남은 처리 시간이 가장 짧은 프로세스에게 CPU를 할당한다.
- SJF를 선점 방식으로 운영하는 것으로 이해하면 된다.
- 잦은 선점으로 인한 문맥 교환의 부담이 있다.

#### 3) MLQ (Multi-level Queue, 다단계 큐)
<br/>
<img width="50%" src="https://velog.velcdn.com/images/wisdom-one/post/f3a685f0-a47f-4ce0-bf3c-0fe0e9b0d3cc/image.png"/>
<br/>

- 프로세스를 우선순위에 따라 나누고, 우선순위 개수만큼의 큐를 이용하여 우선순위가 높은 프로세스가 선점한다.
- `정적 우선순위`를 사용하므로, 큐들 간에 프로세스의 이동이 불가능하다.


#### 4) MFQ(Multi-level Feedback Queue, 다단계 피드백 큐)
<br/>
<img width="50%" src="https://velog.velcdn.com/images/wisdom-one/post/6d2d1b56-51b9-4181-a163-77d083ca41e0/image.png"/>
<br/>

- FCFS와 라운드 로빈 스케줄링 기법을 혼합한 방식.
- 최하위 우선순위의 큐는 라운드 로빈 방식으로, 나머지는 FCFS 방식을 적용한다.
- 각 큐는 서로 다른 시간 할당량을 가지는데, 우선순위가 높은 단계의 큐일수록 시간 할당량을 작도록 한다.
- 새로운 프로세스는 가장 높은 우선순위의 큐에 들어간다.
- 프로세스가 FCFS의 순서로 CPU를 할당받아 실행되는 도중에 시간 할당량이 끝나면, 한 단계 낮은 우선순위의 큐로 이동하게 되고, <br/>
  마지막 단계의 큐는 라운드 로빈 방식으로 CPU를 할당받는다.
- `동적 우선순위`를 기반으로 한다.


<br/>

## 🔖 참고
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/CPU%20Scheduling.md
