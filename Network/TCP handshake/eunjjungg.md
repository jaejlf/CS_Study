# 1. TCP, Transmission Control Protocol

> 인터넷상에서 데이터를 메세지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜 → IP는 배달을, TCP는 패킷의 추적 및 관리를 담당<br/>
TCP는 애플리케이션에게 신뢰적이고 연결지향성 서비스를 제공함<br/>
> 

### TCP 특징

- 3-way handshaking 과정을 통해 연결을 설정하고 4-way handshaking을 통해 연결을 해제함
- 흐름 제어 및 혼잡 제어
- 높은 신뢰성을 보장함
- UDP 보다 속도가 느림
- 전이중(Full-Duplex), 점대점 방식

<br/><br/>

# 2. 3-Way, 4-Way Handshake

> 3-Way Handshake은 TCP의 접속, 4-Way Handshake는 TCP의 접속 해제 과정임
> 


### a. 포트(port) 상태 정보

- CLOSED : 포트가 닫힌 상태
- LISTEN : 포트가 열린 상태로 연결 요청 대기중
- SYN_RCV : SYNC 요청을 받고 상대방의 응답을 기다리는 중
- ESTABLISHED : 포트 연결 상태

<br/>

### b. 플래그 정보

- TCP 헤더에는 CONTROL BIT(플래그 피트, 6bit)가 존재하고 각각의 피트는 URG-ACK-PSH-RST-SYN-FIN
- SYN (Synchronize Sequence Number) / 000010
    - 연결 설정, Sequence Number를 랜덤으로 설정하여 세션을 연결하는 데 사용하며 초기에 Sequence Number를 전송함
- ACK (Acknowledgement) / 010000
    - 응답 확인 (패킷을 받았다는 것을 의미)
    - Acknowledgement Number 필드가 유효한지 나타냄
    - 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 첫 번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정됨
- FIN (Finish) / 000001
    - 연결 해제
    - 세션을 종료시킬 때 사용되며 더 이상 데이터가 없음을 의미
    
<br/><br/>    

# 3. TCP의 3-Way Handshake

> TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 **연결을 설정**(Connection Establish)하는 과정<br/>
양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비가 되었다는 것을 알 수 있도록 함<br/> 
→ TCP/IP 프로토콜을 이용해서 통신하는 응용 프로그램이 데이터 전송 전 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미<br/>
> 

### a. PAR (Positive Acknowledgement with Re-transmission)

![image](https://user-images.githubusercontent.com/100047095/184466801-c716a236-a4cc-460e-a01d-369b88de78f6.png)

출처 : [https://velog.io/@averycode/네트워크-TCPUDP와-3-Way-Handshake4-Way-Handshake](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)

<br/>

- TCP 통신은 PAR 과정을 틍해 신뢰적인 통신을 제공함
- PAR을 사용하는 기기는 ack를 받을 때까지 데이터 유닛을 재전송함
    - 수신자가 데이터 유닛(segment)이 손상된 것을 확인하면 해당 세그먼트를 제거함 → sender는 positive ack이 오지 않은 데이터 유닛을 재전송함 → `이 과정에서 클라이언트와 서버 사이에서 3개의 Segment가 교환됨` → `3-Way Handshake`

<br/>

### b. 3-Way Handshake 작동 방식

1. Client는 Server와 연결하기 위해 3-Way Handshake을 통해 연결 요청을 함 (일반적으로 Client와 Server 모두 연결 요청을 진행할 수 있기 때문에 연결 요청을 먼저 시도한 요청자를 Client, 연결 요청을 받은 수신자를 Server로 생각)  
2. SYN (Synchronization) : 연결 요청, 세션을 설정하는데 사용되며 초기에 시퀀스 번호를 보냄
3. ACK (Acknowledgement) : 보낸 시퀀스 번호에 TCP 계층에서의 길이 또는 양을 더한 것과 같은 값을 ACK에 포함하여 전송
4. 동기화 요청에 대한 답변 : Client의 Sequence Number + 1을 하여 ACK로 돌려줌 

![image](https://user-images.githubusercontent.com/100047095/184466807-52925e16-4c14-4072-abcb-b5169a361c83.png)

출처 : [https://velog.io/@averycode/네트워크-TCPUDP와-3-Way-Handshake4-Way-Handshake](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)

<br/>

### c. 좀 더 자세한 작동 방식

- i. 클라이언트는 서버와 커넥션을 연결하기 위해 SYN을 보냄 (seq: x)
    - 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고 SYN 플래그 비트를 1로 설정한 세그먼트를 전송함
    - PORT 상태
        - Client : `CLOSED` → `SYN_SENT`
        - Server : `LISTEN`
    
- ii. 서버가 SYN(x)을 받고 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 전송함 (seq: y, ACK: x + 1)
    - 접속 요청을 받은 Server가 요청을 수락했으며 접속 요청 프로세스인 Clinet도 포트를 열어달라는 메세지 전송 (SYN-ACK signal bits set)
    - ACK Number필드를 Sequence Number + 1로 설정하고 SYN과 ACK 플래그 비트를 1로 설정한 세그먼트 전송 (seq=y, Ack = x + 1, SYN, ACK)
    - PORT 상태
        - Client : `CLOSED`
        - Server : `SYN_RCV`

- iii. 클라이언트는 서버의 응답으로 ACK(x + 1) & SYN(y) 패킷을 받고 ACK(y+1)을 서버쪽으로 보냄
    - 마지막으로 접속 요청 프로세스 Clinet가 수락 확인(ACK)을 보내 연결을 맺음
    - 이 때 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있음
    - PORT 상태
        - Client : `ESTABLISHED`
        - Server : `SYN_RCV` → ACK → `ESTABLISHED`

- Full-Duplex 통신
    - Step 1, 2에서는 Client → Server 방향에 대한 연결 파라미터(시퀀스 번호)를 설정하고 이를 승인
    - Step 2, 3에서는 Server → Client 방향에 대한 연결 파라미터(시퀀스 번호)를 설정하고 이를 승인

<br/><br/>

# 4. TCP의 4-Way Handshake

> 4-Way Handshake은 연결을 해제(Connection Termination)을 하는 과정임
`FIN` flag를 이용함 : 세션을 종료시킬 때 사용되며, 더 이상 보낸 데이터가 없음을 나타냄
> 

### a. Termination의 종류

1. **Graceful connection release(정상적인 연결 해제**)
    
    상적인 연결 해제에서는 양쪽이 커넥션이 서로 모두 커넥션을 닫을 때까지 연결되어 있음
    
2. **Abrupt connection release(갑작스런 연결 해제**)
    
    갑자기 한 TCP 엔티티가 연결을 강제로 닫거나 한 사용자가 두 데이터 전송 방향을 모두 닫는 경우
    
<br/>

### b. Abrupt 작동 방식

> `RST` 세그먼트가 전송되면 갑작스러운 연결 해제가 수행됨
> 

아래와 같은 경우에 `RST` 세그먼트가 전송됨

- 존재하지 않는 TCP 연결에 대해 비SYN 세그먼트가 수신된 경우
- 열린 커넥션에서 일부 TCP 구현이 잘못된 헤더가 있는 세그먼트가 수신된 경우 → `RST` 세그먼트로 해당 커넥션을 닫아 공격을 방지
- 일부 구현에서 기존 TCP 연결을 종료해야 하는 경우
    - 연결을 지원하는 리소스가 부족할 때
    - 원격 호스트에 연결할 수 없고 응답이 중지되었을 때

<br/>

### c. Graceful 작동 방식

![image](https://user-images.githubusercontent.com/100047095/184466811-a8ae5cf4-3f66-4152-a835-6148e81141e9.png)

출처 : [https://velog.io/@averycode/네트워크-TCPUDP와-3-Way-Handshake4-Way-Handshake](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)

<br/>

- i. **Client → Server : FIN(+ACK)**
    - 서버와 클라이언트가 연결된 상태에서 클라이언트가 close()를 호출하여 접속을 끊으려고 시도
    - 클라이언트는 서버에게 연결을 종료한다는 `FIN` 플래그를 보냄
    - 이 `FIN`

- ii. **Server → Client : ACK**
    - 서버는 `FIN` 패킷을 받고 확인했다는 `ACK` 를 클라이언트에게 보내고 자신의 통신이 끝날 때까지 기다림 (서버는 `TIME_WAIT` 상태가 됨)
    - 서버는 ACK Number 필드를 (Sequence Number + 1)로 지정하고 ACK 플래그 비트를 1로 설정한 세그먼트를 전송
    - 서버는 클라이언트에게 응답을 보내고 `CLOSE_WAIT` 상태에 들어감, 남은 데이터가 있다면 마저 전송을 마친 후 close()를 호출
    - 클라이언트는 서버에서 ACK를 받은 후 서버가 남은 데이터 처리를 끝내고 `FIN` 패킷을 받을 때까지 기다림

- iii. **Server → Client : FIN**
    - 위에서 남은 데이터 처리를 완료하면 서버는 연결 종료에 합의한다는 의미로 `FIN` 패킷을 클라이언트에게 보낸 후 승인 번호를 보내줄 때까지 기다리는 `LAST_ACK` 상태로 들어감

- iv. **Client → Server : ACK**
    - 클라이언트는 `FIN` 을 받고 확인했다는 `ACK` 를 서버에게 보냄
    - 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 `TIME_WAIT` 상태에서 대기 (이후 실질적인 종료과정인 `CLOSED`로 들어가게 됨)
        - TIME_WAIT 상태는 의도치 않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지
        - 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 `CLOSED` 상태로 들어가게 됨

- v. 서버는 ACK를 받은 이후 소켓을 닫는다 (`CLOSED`)

- vi. TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (`CLOSED`)
