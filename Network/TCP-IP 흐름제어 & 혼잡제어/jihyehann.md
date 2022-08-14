# 💡TCP 통신

TCP 통신의 특징은 다음과 같다.

- point-to-point 통신: 하나의 송신 측과 하나의 수신 측이 통신하는 `1:1 통신`이다.
- reliable: 신뢰성 있는 데이터 전송(`RDT`, Reliable Data Transfer)을 한다. 즉, 데이터가 오류 없이 손상되거나 손실되지 않고 전송된다.
- in-order: 순서를 보장한다.
- full duplex(전이중 통신) : 쌍방향 통신이 가능하다. 즉 데이터 송수신이 가능하다.
- connection-oriented : 연결 지향적이다. 송신 측과 수신 측이 데이터를 교환하기 전에 `handshaking`을 한다.

<br/><br/>

# 💡흐름 제어 (Flow Control)

TCP의 경우, 각 connection 별로 버퍼가 존재한다. 

만약 송신 측에서 너무 빠르게 패킷을 전송하여 수신 버퍼가 가득 차게 된다면(overflow), 전송한 데이터가 손실될 것이다.

이런 상황을 대비하기 위해, 수신 측에서 송신 측의 데이터 전송 속도를 조절하는데, 이것을 흐름 제어라고 한다.

<br/>

## ✔️ Stop and Wait

- 패킷을 전송한 후, 확인 응답을 받을 때까지 기다렸다가, 확인 응답을 받은 후에 그 다음 패킷을 전송하는 방법이다.

![image](https://user-images.githubusercontent.com/75151848/184527764-396be37a-f9fc-4a86-909b-57c80f54c048.png)

<br/>

## ✔️ Sliding Window (Go Back N ARQ)

- 수신 측에서 설정한 윈도우 크기만큼 송신측에서 확인 응답없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 제어기법이다.

![image](https://user-images.githubusercontent.com/75151848/184529184-7b3406c7-4576-46b7-bb11-569755440aa9.png)


- LastByteSent: 마지막으로 전송된 바이트
- LastByteAcked: 마지막으로 확인된 바이트
- ReceiveWindowAdvertised: 슬라이딩 윈도우 크기 (여유 공간)
- `LastByteSent - LastByteAcked <= ReceiveWindowAdvertised` 이면 overflow가 아님을 보장할 수 있다.

### **윈도우 크기**

- 최초의 윈도우 크기는 **3 way handshaking**을 통해 수신 측 윈도우 크기로 설정된다.
- 윈도우 크기는 이후 수신 측의 버퍼에 남아있는 공간에 따라 변한다.
- 윈도우 크기는 수신 측에서 송신 측으로 확인 응답(**ACK**)을 보낼 때 **TCP 헤더(window size)에 담아서 보낸다**(advertise).

### 재전송

- 송신 측은 일정 시간 동안 수신 측으로부터 확인 응답(ACK)을 받지 못하면, 패킷을 재전송한다.

<br/><br/>

# 💡혼잡 제어 (Congestion Control)

혼잡(Congestion)은 네트워크 내에 패킷의 수가 과도하게 증가하는 현상을 말한다.

혼잡 제어란, 네트워크 상의 혼잡을 줄이기 위해 패킷의 전송량을 조절하는 것을 말한다.

흐름 제어가 송신측과 수신측 사이의 전송 속도를 다루는데 반해, 혼잡 제어는 호스트와 라우터를 포함한 보다 넓은 관점에서 전송 문제를 다룬다.

<br/>

## ✔️ AIMD(Additive Increase / Multiplicative Decrease)

![image](https://user-images.githubusercontent.com/75151848/184531794-1bae030f-e1e1-45ac-9661-6970dffc8436.png)

- `additive increase`: 처음에 패킷을 하나씩 보내고 이것이 문제없이 도착하면 window 크기(단위 시간 내에 보내는 패킷의 수)를 1씩 증가시켜가며 전송한다. (**`선형적 증가`**)
- `multiplicative decrease`: 패킷 전송에 실패하거나 일정 시간을 넘으면 패킷의 보내는 속도를 `절반으로 줄인다.`
- **문제점:** 초기에 네트워크의 높은 대역폭을 사용하지 못하여 오랜 시간이 걸리게 되고, 네트워크가 혼잡해지는 상황을 미리 감지하지 못한다. 즉, 네트워크가 혼잡해지고 나서야 대역폭을 줄이는 방식이다.

<br/>

## ✔️ Slow Start

- AIMD와 마찬가지로 패킷을 하나씩 보내면서 시작하고, 패킷이 문제없이 도착하면 각각의 ACK 패킷마다 window size를 1씩 늘려준다. 즉, 윈도우의 크기가 1,2,4,8,… 과 같이 **`지수적으로 증가`**한다.
- 초기 window size : 1
- 매 RTT마다 window size를 2배로 증가시킨다. ( ex : 1, 2, 4, 8, 16...)
- 패킷 손실을 감지하면 window size를 1 로 줄인다.

<br/>

## ✔️ TCP Tahoe

![image](https://user-images.githubusercontent.com/75151848/184531805-92395862-db67-4751-8395-451d8ea12b14.png)

처음에는 Slow Start를 사용하다가 임계점(ssthresh)에 도달하면 AIMD 방식을 사용한다.

- 처음 window size: 1 이다.
- 임계점까지는 Slow Start를 사용한다(window size가 2배씩 증가한다)
- 임계점부터는 AIMD 방식을 사용한다(window size가 1씩 증가한다)
- 3 duplicate ACKs 혹은 timeout을 만나면 임계점을 window size의 절반으로 줄이고 window size를 1로 줄인다.
- `Fast Retransmit`: 3 duplicate ACK를 받게되면, 패킷 손실로 간주하고 timeout을 기다리지 않고 즉지 재전송한다.

<br/>

## ✔️ TCP **Reno**

> TCP Tahoe 방식은 3 duplicate ACKs를 만나고 window size가 다시 1부터 키워나가야 하므로 속도가 느리다. 이를 해결할 수 있는 방식이 TCP Reno이다.
> 
> TCP Reno는 TCP Tahoe와 비슷하지만 3 dupicate ACKs와 timeout을 구분한다.
> 

![image](https://user-images.githubusercontent.com/75151848/184531807-2443c71a-c16b-46b8-becf-7265fec59a31.png)
- 처음 window size는 1 이다.
- 임계점(ssthresh)까지는 Slow Start를 사용한다(window size가 2배씩 증가한다)
- 임계점부터는 AIMD 방식을 사용한다(window size가 1씩 증가한다)
- 3 duplicate ACKs를 만나면 window size를 절반으로 줄이고(`Fast Recovery`) 임계점을 그 값으로 설정한다. AIMD 방식으로 동작한다.
- timeout을 만나면 window size를 1로 줄인다. 임계점은 변하지 않는다.
- `Fast Recovery`: `Fast Retransmit` 수행 후 Slow Start가 아닌 Congestion Avoidance(AIMD) 상태에서 전송한다.

<br/>

![image](https://user-images.githubusercontent.com/75151848/184529663-a3a823be-e92c-41ae-a566-5c9979d988fa.png)

<br/><br/>

## 📌 참고

- [https://code-lab1.tistory.com/28](https://code-lab1.tistory.com/28)
- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Network/TCP (흐름제어혼잡제어).md#tcp-흐름제어혼잡제어](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%20(%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4).md#tcp-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4)
- [https://www.brianstorti.com/tcp-flow-control/](https://www.brianstorti.com/tcp-flow-control/)
- [https://steady-coding.tistory.com/507](https://steady-coding.tistory.com/507)
- [https://code-lab1.tistory.com/30](https://code-lab1.tistory.com/30)
