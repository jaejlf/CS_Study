# TCP 3 & 4 Way Handshake

## A. 선행 지식

<br>

### TCP(Transmission Control Protocol)란?

서버와 클라이언트간 데이터 전송의 신뢰성을 보장하는 역할을 담당한다.

데이터는 네트워크 선로를 통해 전달되는 과정 속에서 손실되거나 순서가 뒤바뀌어 전송될 수 있는데 TCP는 이런 손실을 검색하고 교정하여 순서를 재조합할 수 있도록 도와준다.

TCP는 **연결형 프로토콜**로, 연결이 미리 설정되어 있어야지만 통신이 가능하다.

**신뢰성 있는 데이터 전송**을 하며,
**1: 1(Unicast)** 통신을 한다.

<br>

#### 추가 지식

- TCP, UDP: 전송 계층에서 사용하는 프로토콜로, **패킷을 상위 특정 응용 프로그램에 전달**하는 것에 목적이 있다.
  전송 방식으로는 TCP와 UDP가 있다. - TCP, UDP 공통점: - 포트 번호를 이용하여 주소 지정 - 데이터 오류 검사를 위한 체크섬 존재

- 전송 계층: 송신자와 수신자를 연결하는 통신 서비스 제공, IP에 의해 연결되는 패킷의 오류 검사, 재전송 요구 제어 담당

<br>

### TCP 헤더

TCP는 응용 계층으로부터 받은 데이터에 헤더를 추가한 뒤, 하위 계층으로 전달한다.

<img src="https://cdn.kastatic.org/ka-perseus-images/ec71832edb1f2ff1d2ad12da494033ce2b25aafa.svg">

<br>

- **일련 번호(Sequence number)**: 32bit. 송신자가 지정하는 순서 번호.
  - 전송되는 바이트 수를 기준으로 증가한다.
  - 이를 통해, TCP에서는 신뢰성 및 흐름제어 기능 제공(슬라이딩 윈도우)
- **확인 번호(Acknowledgement number)**: 32bit. 수신하기를 기대하는 다음 바이트 번호.
  - 마지막 수신 성공 일련 번호(Sequence Number) + 1
- **6개의 플래그 비트(Flag Bit)**: TCP 세그먼트 전달과 관련하여 TCP 회선 및 데이터 관리 기능을 담당한다.
  - URG(Urgent): 긴급 위치 필드의 유효 여부 판단
  - ACK(Acknowledgement): 확인 필드에 확인 번호(Acknowledgement Number) 값이 셋팅됐음을 알림.<br> 1이면 유효, 0이면 미포함.
    - TCP 연결 이후 전송되는 모든 세그먼트에서는 항상 이 비트가 1로 설정
  - PSH(Push): 버퍼링 된 데이터를 가능한 한 빨리 상위 계층에 전달할 것
  - RST(Reset) : 연결의 리셋이나 유효하지 않은 세그먼트에 대한 응답용
  - SYN(Synchronize) : 연결 설정 요구. 동기화 시퀀스 번호
    - 양쪽이 보낸 최초의 패킷에만 이 플래그가 설정되어야 함
  - FIN(Finish) : 더 이상 전송할 데이터가 없을 때, 연결 종료 의사 표시
- 윈도우 크기(Window Size): 16비트. 한번에 전송할 수 있는 데이터의 양
- 체크섬(Checksum): 데이터를 송신하는 중에 발생할 수 있는 오류를 검출하기 위한 값
- 긴급 포인터(Urgent Pointer): 긴급 포인터. URG 플래그가 1이라면 수신 측은 이 포인터가 가르키고 있는 데이터를 우선 처리
- 옵션(Option): TCP의 기능을 확장할 때 사용하는 필드. 크기가 가변적

---

<br>

## B. TCP 3-way handshake, TCP 4- way handshake

TCP는 신뢰성을 보장하기 위해 장치들 사이에 논리적인 접속을 성립(establish)한다.

3-way handshake는 데이터를 전송하기 위해 **네트워크 연결을 설정**하는 과정이고, 4-way handshake는 **TCP의 연결을 해제**하는 과정이다.

<br>

### 3 - way handshake 과정

<br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWsCO3%2FbtrHqodOWEm%2FYboNOvS96hTTZrkxJQlLQ1%2Fimg.png" height=170>

<br>

#### 1단계: 클라이언트 → 서버(SYN)

클라이언트가 서버에게 SYN 플래그가 1로 설정된 패킷을 전송한다. (SYN = "synchronize?")

- 클라이언트의 일련번호(Sequence number, 이하 seq)는 최초 설정이므로 임의의 랜덤 숫자로 정해진다.

```
ex) seq: 7001(랜덤 숫자)
    ack: 미설정
    SYN 플래그: 1
    ACK 플래그: 0
```

#### 2단계: 서버 → 클라이언트(SYN/ACK)

서버는 클라이언트에게 접속 요청을 수락했으며(ACK = "Acknowledge!"), 클라이언트도 포트를 열어 달라는 메세지를 전송한다(SYN)

- ACK = 1
- SYN = 1
- seq: 서버 역시 최초 설정이므로 일련번호가 임의의 숫자로 정해진다.
- 서버의 확인 번호(Acknowledgement number, 이하 ack)는 클라이언트에게 마지막으로 전송받은 seq +1 로 설정된다

```
ex) seq: 3001(랜덤 숫자)
    ack: 7002
    -> client의 seq + 1
    SYN 플래그: 1
    ACK 플래그: 1
```

#### 3단계: 클라이언트 → 서버 (ACK)

클라이언트는 '서버로부터 전달받은 'SYN-ACK' 패킷을 정상 수신하였다"는 의미의 수신 확인 패킷인 'ACK' 패킷을 만들어 서버로 다시 전송한다.

이 이후로부터는 데이터 전송이 가능하다.

```
ex) seq: 7002
    ack: 3002
    -> server의 seq + 1
    SYN 플래그: 0
    ACK 플래그: 1
```

<br>

이렇게 세 번의 통신이 완료되면 연결이 성립한다.

<br>

##### 번외

+) 데이터 전송은 어떻게 이루어지나요❓

<img src="https://cdn.kastatic.org/ka-perseus-images/2cfc6b88b3b5c3a27386503d347524c2065a57d9.svg" height = 150>

이후에는 데이터를 전송하는 컴퓨터가 일련 번호(seq)와 데이터를 담은 패킷을 전송한다.

수신한 컴퓨터는 데이터를 받았다는 의미에서 ACK 플래그를 1로 설정하고, 확인 번호(ack)를 수신한 데이터의 크기만큼 증가시킵니다.

- three-way handshake와 달리 데이터 전송 때는
  확인 번호(ack) = 이전 전송패킷의 일련번호(seq) + 데이터 크기

```
데이터 전송 시에는 일련 번호(Sequence number)와 확인 번호(Acknowledgement number)
```

<br>

### 4 - way handshake

<br>

<img src="https://media.geeksforgeeks.org/wp-content/uploads/CN.png">

TCP와의 연결을 해제하는 과정이다.

<br>

#### 1단계: 클라이언트 → 서버(FIN)

클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다.

#### 2단계: 서버 → 클라이언트 (ACK)

서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보낸다. (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다)

#### 3단계: 서버 → 클라이언트 (FIN)

데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보낸다.

#### 4단계: 클라이언트 → 서버 (ACK)

서버로부터 받지 못한 데이터가 있을 수 있으므로, TIME_WAIT 상태로 기다린 후, 클라이언트는 확인했다는 ACK 플래그를 전송한다.

- 서버는 ACK를 받은 이후, 소켓을 닫는다.(Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다.(Closed)

<br>

이렇게 네 번의 통신이 완료되면 연결이 완료된다. (정상 종료)

<br>

## C. 기타 질문

<br>

Q1. Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN패킷보다 늦게 도착하는 상황"이 발생한다면 어떻게 될까요?

A1. Client에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop 되고 데이터는 유실될 것입니다.

이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도 일정 시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 "TIME_WAIT" 라고 합니다.

Q2. 연결 과정에서 초기 일련 번호를 랜덤 번호로 사용하는 이유는?

A2. 커넥션을 맺을 때 사용하는 포트는 **유한 범위**내에서 사용하기 때문이다. 따라서 이미 사용했던 포트 번호 쌍을 다시 재사용할 가능성이 존재한다.

서버 측에서는 패킷의 일련 번호(seq)를 보고 패킷을 구분하게 되는데, 이때 난수가 아니라 순차적인 번호가 전송된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수가 있다. 이런 문제가 발생할 가능성을 줄이기 위해 난수로 설정한다.

<br>

---

## D. 참고자료

🔗 https://100100e.tistory.com/267

🔗 http://www.ktword.co.kr/test/view/view.php?m_temp1=1889

🔗 https://www.khanacademy.org/computing/computers-and-internet/xcae6f4a7ff015e7d:the-internet/xcae6f4a7ff015e7d:transporting-packets/a/transmission-control-protocol--tcp
