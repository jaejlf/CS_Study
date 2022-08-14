# OSI 7계층

## A. OSI 7 계층이란?

<img src="https://miro.medium.com/max/1400/1*tnEkvHfXNnhv7xAthT2sJQ.png">

<br>

#### OSI(Open System Interconnection Reference Model) 참조 모델

<br>

ISO라는 국제 표준화 기구에서 개발한 모델로, 컴퓨터 네트워크에서 사용하는 프로토콜과 프로토콜을 지원하기 위한 기능들을 계층 구조로 나누어서 설명할 때 사용하는 모델

계층 구조로 구성되어 있기 때문에 보통 **'OSI 7계층 모델** 이라고 한다.

유닉스와 같은 컴퓨터 장비는 OSI 7 계층이 만들어지기 이전부터 사용하였기 때문에 리눅스 운영체제를 따르는 대다수의 컴퓨터 운영체제는 OSI 참조 모델을 따르지 않는다.

> OSI 참조 모델은 표준이 아닌 참조 모델이란 이름으로 단순히 참조하는 형태로 사용된다!

### 1계층 - 물리 계층(Phyisical Layer)

네트워크 데이터가 전송되는 물리적인 매체

물리적으로 연결된 두 대의 컴퓨터가 0과 1의 나열을 주고받을 수 있게 해주는 모듈(module)

- PDU(Protocol Data Unit) - Bit
- 예시: 전압, 허브 , 네트워크 어뎁터, 중계기 및 케이블 사양, 신호 변경

<br>

### 2계층 - 데이터링크 계층(Data Link Layer)

물리 계층으로 송수신되는 정보를 관리하여 안전하게 전달되도록 도와주는 역할 수행(데이터의 무결성 검증)

같은 내트워크에 있는 컴퓨터들이 데이터를 주고받기 위해 필요한 모듈

Framing → Data Link Layer에 속하는 작업 중 하나<br>
(Framing: 특정 비트열로 데이터 감싸는 것)

- PDU(Protocol Data Unit) - Frame
- 예시: MAC 주소, 브리지 및 스위치

+)
스위치: 목적지 확인 후 특정 수신자에게 메세지 갈 수 있도록 한다<br>

라우터: 스위치와 스위치를 연결하여 서로 다른 네트워크에 속한 컴퓨터끼리 통신이 가능하게 해주는 장치

<br>

### 3계층 - 네트워크 계층(Network Layer)

실제 네트워크 간의 라우팅을 담당하여 최적의 경로에 따라 패킷을 전달. 흐름제어, 오류제어 등을 수행.

수많은 네트워크의 연결로 이루어진 Inter-network 중 어딘가에 있는 목적지 컴퓨터로 데이터를 전송하기 위해

✔️ IP 주소를 이용해서 길을 찾고(Routing)

→ 이를 위해 목적지와 소스로 구분되는 컴퓨터를 식별하는 데 사용되는 IP 주소가 패킷의 헤더에 들어간다

✔️ 자신 다음의 라우터에게 데이터를 넘겨주는 것(fowarding)

- PDU(Protocol Data Unit) - Packet
- 예시: 라우터

<br>

### 4계층 - 전송 계층(Transport Layer)

네트워크를 통해 주고 받는 데이터에 대해 **신뢰성**(Reliable delivery in real-time)을 보장하는 기능 제공

**신뢰성이 보장되는 시스템** - 발신자가 전송한 데이터를 주어진 시간 내 오류 없이 그대로 전달하는 기능 수행

TCP, UDP 프로토콜 존재.

전송 과정에서 발생할 수 있는 프레임이나 패킷의 유실 여부 확인 위해 패킷 내 **전달 순서** 표시하여 전달

- PDU(Protocol Data Unit) - TCP: Segment, UDP: Datagram
- 예시: 특정 방화벽 및 프록시 서버

<br>

### 5계층 - 세션 계층(Session Layer)

데이터가 통신하기 위한 논리적 연결을 담당하여, TCP/IP 세션을 만들고 없애는 역할을 수행

- PDU(Protocol Data Unit) - Data

+) 세션(Session)

발신자와 수신자의 역할을 하는 두 대의 컴퓨터가 서로 **논리적으로 연결되어 있다**

Unix나 Linux의 커널에서는 지원 ❌

<br>

### 6계층 - 표현 계층(Presentation Layer)

데이터를 암호화, 인코딩

- PDU(Protocol Data Unit) - Data
- 예시: 인코딩, 디코딩, 복호화, 암호화

### 7계층 - 응용 계층(Application Layer)

최종 목적지로, 사용자가 응용 서비스를 수행할 수 있다

일반 애플리케이션을 의미하기 보다 애플리케이션 프로토콜을 사용하는 계층을 의미

ex) HTTP 프로토콜, SMTP 프로토콜, FTP 프로토콜

- PDU(Protocol Data Unit) - Data
- 예시: 텔넷, 구글 크롬 이메일, 데이터베이스 관리

## B. (추가) TCP/IP 모델은?

<br>

<img src="https://velog.velcdn.com/images%2Famuse%2Fpost%2Fa1ebe066-47dc-4479-b465-dda2494a1efd%2Fsimilarities-and-differences-between-osi-and-tcp-ip-model.png">

TCP/IP 모델 역시 OSI 7계층처럼 네트워크 시스템에 대한 모델. 현재는 OSI 모델보다 TCP/IP 모델의 점유율이 더 높다.

> 현재는 TCP/IP Updated 모델 사용!

<br>

## C. 참고 자료

🔗 https://velog.io/@amuse/OSI-7-Layers

📚 기적을 부르는 안드로이드 통신 프로그래밍 제 3판 - 박현재
