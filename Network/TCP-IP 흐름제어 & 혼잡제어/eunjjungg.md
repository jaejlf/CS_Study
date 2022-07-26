# 1. 용어 정리

- Timeout : 여러가지 요인으로 인해 송신 측이 보낸 데이터 자체가 유실되었거나 수신 측이 응답으로 보낸 `ACK` 가 유실되는 경우를 말함
- 3 ACK Duplicate (뒤에 혼잡 제어에 등장) : 패킷을 받는 수신자 입장에서는 세그먼트로 분할된 내용들이 순서대로 도착하지 않는 경우가 있음 → 잘 도착한 마지막 패킷의 다음 순번을 `ACK` 패킷에 실어서 보냄. 이런 중복 `ACK` 3개를 받으면 문제가 있다고 판단하여 해당 패킷을 송신 측이 재전송함

<br/><br/>

# 2. 흐름 제어

> 수신 측이 송신 측보다 데이터 처리 속도가 느린 경우 문제가 생김<br/>
수신 측에서 제한된 저장 용량을 초과한 이후 도착한 패킷들은 손실될 수 있으며 손실된다면 불필요한 추가 패킷 전송이 발생하게 됨<br/>
이와 같이 송신 측과 수신 측의 TCP 버퍼 크기 차이로 인해 생기는 데이터 처리 속도 차이를 해결하기 위한 기법이 **흐름 제어** 기법<br/>
**TCP 버퍼** : 송신 측은 버퍼에 TCP 세그먼트를 보관한 후 순차적으로 전송하고, 수신 측은 도착한 TCP 세그먼트를 애플리케이션이 읽을 때까지 버퍼에 보관함<br/>
> 

<br/>

### a. Stop and Wait

> 매번 전송한 패킷에 대해 확인 응답 `ACK` 을 받으면 다음 패킷을 전송하는 방법<br/>
> 패킷을 하나씩 보내기 때문에 비효율적인 방법임
> 

![image](https://user-images.githubusercontent.com/100047095/184470890-c2f2295b-264d-4633-8cd0-4b6a0466d16d.png)

<br/>

### b. Sliding Window

> 수신 측에서 설정한 윈도우 크기만큼 송신 측에서 확인 응답 `ACK` 없이 패킷을 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 제어 기법
> 

> 윈도우 크기 : 최초의 윈도우 크기는 호스트들의 3-Way HandShaking 기법을 통해 수신 측 윈도우 크기로 설정되며 이후 수신 측의 버퍼에 남아 있는 공간에 따라 변함<br/>
> 윈도우 크기는 수신 → 송신으로 확인 응답 `ACK`를 보낼 때 TCP 헤더에 담아서 보냄 <br/>
→ 윈도우는 메모리 버퍼의 일정 영역<br/>
> 

<br/>

**동작 방식**

> 윈도우에 포함된 패킷을 모두 전송하고 수신 측으로 확인 응답 `ACK` 이 오면 윈도우를 옆으로 옮겨 다음 패킷들을 전송함
> 

![image](https://user-images.githubusercontent.com/100047095/184470900-7ff376b7-d7fd-453f-9347-2ca2f4458157.png)

<br/>

**전송 과정**

- 최초로 수신자는 윈도우 사이즈를 7로 정함
- 송신자는 수신자의 확인 응답 `ACK` 를 받기 전까지 데이터를 보냄
- 수신자는 확인 응답 `ACK` 를 송신자에게 보내면 슬라이딩 윈도우 사이즈를 충족할 수 있게끔 윈도우를 옆으로 옮김
- 이후 데이터를 다 받을 때까지 위 과정 반복
- 송신 측은 일정 시간 동안 수신 측으로부터 확인 응답 `ACK` 을 받지 못하면 패킷을 재전송함 → 송신측에서 재전송 요청을 보냈는데 패킷이 소실된 것이 아니고 수신 측의 버퍼에 남는 공간이 없는 경우라면 문제 발생 → 이를 해결 위해 송신 측은 해결 응답 ACK를 보내면서 남은 버퍼의 크기(윈도우 크기)도 같이 전송함

<br/><br/>

# 3. 혼잡 제어

> 데이터의 양이 라우터가 처리할 수 있는 양을 초과하면 초과된 데이터는 라우터가 처리하지 못함 <br/>
> → 이때 송신 측에서는 라우터가 처리하지 못한 데이터를 손실 데이터로 간주하고 계속 재전송하여 네트워크를 혼잡하게 함 <br/>
> → 송신 측의 전송 속도 조절로 예방 가능 <br/>
> → 이 과정이 혼잡 제어 기능임<br/>
네트워크 내의 패킷 수를 조절하여 네트워크의 오버플로우를 방지하는 기능
> 

<br/>

### a. AIMD (Additive Increse/Multicative Decrease)

> 합 증가/곱 감소 방식
> 
- 처음에 패킷을 하나씩 보내고 문제 없이 도착하면 윈도우의 크기를 1씩 증가시켜가며 전송함 → 만약 전송에 실패하면 윈도우 크기를 반으로 줄임
- 단점 : 윈도우 크기를 너무 조금씩 늘려 네트워크의 모든 대역을 활용하여 제대로 된 속도로 통신하기까지 오래 걸림

![image](https://user-images.githubusercontent.com/100047095/184470905-e7aef54c-c86a-4a4e-ab8a-8545f2352fa5.png)

<br/>

### b. Slow Start

> 느린 시작
> 
- AIMD 방식은 윈도우 크기를 선형적으로 증가시키므로 제대로 된 속도를 내기까지 오래 걸리지만 Slow Start는 윈도우의 크기를 1, 2, 4, 8과 같이 지수적으로 증가시키다가 혼잡이 감지되면 윈도우 크기를 1로 줄이는 방식임
- 보낸 데이터의 `ACK` 가 도착할 때마다 윈도우 크기를 증가시키기 때문에 처음에는 윈도우 크기가 조금 느리게 증가해도 시간이 지날수록 윈도우 크기가 빠르게 증가

![image](https://user-images.githubusercontent.com/100047095/184470911-f00b3608-492a-4e83-b635-236f6ecc0d5d.png)

<br/>

### c. Fast Retransmit

> 빠른 재전송
> 
- 패킷을 받는 수신자 입장에서 세그먼트로 분할된 내용들이 순서대로 도착하지 않는 경우가 생길 수 있음 → 수신 측에서 순서대로 잘 도착한 마지막 패킷의 다음 순번을 `ACK` 패킷에 실어서 보냄→ 중복 `ACK` 를 3개 받으면 재전송이 이루어짐
- 송신 측은 자신이 설정한 타임 아웃 시간이 지나지 않았어도 바로 해당 패킷을 재전송할 수 있으므로 빠른 재전송률을 유지할 수 있음

<br/>

### d. Fast Recovery

> 빠른 회복
> 
- 빠른 회복은 혼잡한 상태가 되면 윈도우 크기를 1로 줄이지 않고 반으로 줄이고 선형 증가 시킴
- 혼잡 상황을 한 번 겪고부터는 AIMD (1씩 선형 증가시키는 것) 방식으로 동작함
