# 💡 OSI 모형
`Open Systems Interconnection Reference Model`
<br/>

![image](https://user-images.githubusercontent.com/75151848/184472317-50e7a456-77f5-4c1d-9ae4-32bc3233d0a4.png)

국제표준화기구(ISO, International Organizationa for Standardization)에서 개발한 모델로, 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명한 것을 말한다.  
일반적으로 `OSI 7 계층`이라고 한다.

이 모델의 각 계층은 하위 계층의 기능을 이용하고, 상위 계층에게 기능을 제공한다.

## Q. OSI 7 계층을 나눈 이유는 무엇인가?

컴퓨터 네트워크 통신을 계층화하면, 통신이 일어나는 과정을 단계별로 파악할 수 있다는 이점이 있다.

또한 통신 과정 중에 특정한 곳에 이상이 생길 경우, 다른 단계의 장비 및 소프트웨어 등을 건드리지 않고 통신 장애를 일으킨 단계에서 해결할 수 있다.

그리고 계층화는 특정 계층이 제공하는 서비스의 구현을 변경하는 것도 쉽다. 한 계층이 상위 계층에 같은 서비스를 제공하고 하위 계층의 서비스를 이용하기만 하면 해당 계층의 구현이 변경되어도 시스템 나머지 부분은 변경할 필요가 없다.

<br/><br/>

# 1. **Physical Layer (물리 계층)**

> 리피터, 케이블, 허브 등
> 

물리 계층은 OSI 7계층의 최하위 계층으로, 통신 케이블을 통해 전기 신호를 사용하여 `비트 스트림`을 전송하는 계층이다.

이 계층은 전압, 허브, 네트워크 어댑터, 중계기 및 케이블을 비롯해 사용된 모든 하드웨어의 물리적 및 전기적 특성을 정의한다.

디지털 신호에서 아날로그 신호로 또는 아날로그 신호에서 디지털 신호로 변환하는 역할을 한다.

이 계층은 전기 신호를 주고받는 것을 목적으로 하고, 데이터의 종류나 오류 확인은 하지 않는다.

<br/><br/>

# 2. DataLink **Layer (데이터링크 계층)**

> 브릿지, 스위치 등
> 

데이터링크 계층은 **물리계층을 통해 송수신되는 정보의 `오류`와 `흐름`을 관리하여 안전한 정보의 전달을 수행**할 수 있도록 도와주는 역할을 한다.

대부분의 경우, 데이터링크 계층은 네트워크 인터페이스 카드(network interface card, NIC)로 알려진 네트워크 어댑터에 구현된다. 네트워크 어댑터의 중심에는 링크 계층 제어기가 있으며, 이것은 링크 계층 서비스들의 대다수가 구현되어 있는 특수 용도 칩이다.

대표적인 프로토콜로는 `Ethernet` 이 있다.


## MAC 주소

데이터링크 계층은 물리적 주소인 `MAC 주소` (Media Access Control Address)를 가지고 통신을 한다.

이것은 네트워크 인터페이스에 할당된 고유 식별자이고, 길이는 6바이트(48비트)이다. 

MAC 주소는 대체적으로 NIC의 제조업체가 할당하며 하드웨어에 저장된다. 호스트나 라우터가 여러 개의 NIC를 가진 경우, 여러 개의 MAC 주소를 갖게 된다.

## Framing (프레임화)

데이터그램을 캡슐화하여 프레임 단위로 만들고 헤더와 트레일러를 추가하는 것을 말한다.

캡슐화된 데이터를 프레임(frame)이라고 한다.

- 헤더(Header): 출발지 주소, 목적지 주소, 데이터 내용을 정의한다.
- 트레일러(Trailer): 비트의 에러를 감지한다.

## Flow Control (흐름 제어)

송수신자 간 데이터를 처리하는 속도 차이를 해결하기 위한 제어를 담당한다.

## Error Control (오류 제어)

프레임 전송 시에 발생한 오류를 `검출`하고 `복원`하거나 `재전송`한다.

오류 검출 기술로는, **순환중복검사(cyclic redundancy check, `CRC`) 코드**가 널리 사용된다.

<br/><br/>

# 3. Network Layer (네트워크 계층)

> 라우터, IP
> 

네트워크 계층은 데이터를 목적지까지의 경로를 찾아(`routing`) 전달(`forwarding`)하는 계층이다. 

네트워크 계층의 대표적인 장비는 `라우터`이고, 스위치에 라우팅 기능을 장착한 `L3 스위치`도 있다.

## IP (Internet Protocol)

IP는 **주소 지정**과 **데이터 전송**을 담당하는 하나의 프로토콜이다.

네트워크 계층에서 각각의 노드를 식별하는 식별자가 `IP 주소`이다. 주소 체계는 IPv4와 IPv6가 존재한다.

`Best-Effort Service`를 제공한다.

→ 오류 제어, 흐름 제어 기능이 전혀 없다.

<br/><br/>

# 4. Transport Layer (전송 계층)

> TCP, UDP

전송 계층은 종단간(end-to-end) 통신을 다루는 최하위 계층으로, 애플리케이션 **프로세스들 간의 논리적 통신**을 제공한다. (네트워크 계층은 호스트 사이의 논리적 통신을 제공한다.)

대표적인 프로토콜은 `TCP`와 `UDP`가 있다.

## TCP (Transmission Control Protocol)

- 신뢰성 있고, 순서가 보존되고, 연결 지향형 전송 시스템
- Congestion Control(혼잡 제어), Flow Control(흐름 제어), Connection Setup(연결 설정) 등 각종 오류를 제어한다.
- 웹 브라우저들이 월드 와이드 웹에서 서버에 연결할 때 사용되며, 이메일 전송, 파일 전송에도 사용된다.

## UDP (User Datagram Protocol)

- 신뢰성 없고, 순서가 보장되지 않고, 비연결형 전송 시스템
- 꼭 필요한 기능(전송)만 하고, 오류 제어와 같은 추가 기능을 필요로 하지 않는 애플리케이션에 사용된다.
- 추가 기능이 없기 때문에 오버헤드가 작고 지연 시간이 짧다는 장점이 있다.
- 실시간이 중요한 스트리밍 멀티미디어와 같은 응용프로그램, 도메인 네임 서버(DNS) 및 SNMP에 이용된다.
- 인터넷 전화, 화상 회의, 오디오/비디오 스트리밍 등에 사용된다.

## **Multiplexing & Demultiplexing**

- 네트워크 소켓 (Network Socket) : 컴퓨터 네트워크의 사이에 있는 프로세스 간 통신의 종착점이다. 컴퓨터 간 통신의 대부분은 IP(인터넷 프로토콜)을 기반으로 하고 있고, 네트워크 소켓의 대부분은 인터넷 소켓이다. 네트워크 통신을 위해서 송,수신측에서는 소켓을 생성하고, 이 소켓을 통해 서로 데이터를 교환한다.
- Multiplexing(다중화) at Sender : 다수의 소켓들로부터 추가 정보(목적지 주소 등)를 얻어서 전송할 데이터의 헤더에 해당 정보(목적지 주소 등)를 추가하는 기능.
- Demultiplexing(역다중화) at Receiver : 수신된 데이터를 적절한 소켓으로 전달하기 위해 헤더 정보를 이용한다. 하위 계층에서 상위 계층으로 올라갈 때마다 헤더가 작아지면서 전송할 데이터가 목적지에 도착한다.

<br/><br/>

# 5. **Session Layer (세션 계층)**

> API, Socket
> 

세션 계층은 네트워크상 양끝단 연결을 관리하고 연결을 지속시켜주는 계층이다. 

`세션 설정`, `유지`, `종료`, 전송 중단 시 `복구` 등의 기능이 있으며, TCP/IP 세션을 만들고 없애는 책임을 진다.

동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신과 함께, 체크 포인팅과 유휴, 종료, 다시 시작 과정 등을 수행한다. 

<br/><br/>

# 6. **Presentation Layer (표현 계층)**

> JPEG, MPEG 등

표현 계층은 응용 계층으로부터 전달받거나 전송하는 데이터의 `인코딩` 및 `디코딩`을 수행한다.

코드 간의 번역을 담당하여 응용 계층에서 데이터 형식상의 차이를 다루는 부담을 덜더준다.

`MIME 인코딩`이나 `암호화` 등의 동작이 이루어진다.

<br/><br/>

# 7. **Application Layer (응용 계층)**

> HTTP, FTP, DNS 등
> 

응용 계층은 최상위 계층으로, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.

응용 서비스는 관련된 응용 프로세스들 사이의 전환을 제공한다.


<br/><br/>


|  | 계층 | 데이터 단위 | 프로토콜 | 장비 |
| --- | --- | --- | --- | --- |
| 1 | 물리 계층 | Bit | 10BASE-T, 100BASE-TX, ISDN, wired, wireless, RS-232, DSL, Twinax | 허브, 리피터, 케이블 |
| 2 | 데이터링크 계층 | Frame | Ethernet, Token Ring, AppleTalk, PPP, ATM, MAC, HDLC, FDDI, LLC, ALOHA | 브릿지, L2 스위치 |
| 3 | 네트워크 계층 | Packet (Datagram) | IP, IPX, IPsec, ICMP, ARP, NetBEUI, RIP, BGP, DDP, PLP | 라우터, L3 스위치 |
| 4 | 전송 계층 | Segment | TCP, UDP, SPX, SCTP, NetBEUI, RTP, ATP, NBP, AEP, OSPF | 게이트웨이 |
| 5 | 세션 계층 | Data | NetBIOS, SAP, SDP, PIPO, SSL, TLS, NWLink, ASP, ADSP, ZIP, DLC |  |
| 6 | 표현 계층 | Data | ASCII, MPEG, JPEG, MIDI, EBCDIC, XDR, AFP, PAP |  |
| 7 | 응용 계층 | Data | HTTP, SMTP, SSH, FTP, Telnet, DNS, modbus, SIP, AFP, APPC, MAP |  |

<br/><br/>

## 📌 참고

- [https://ko.wikipedia.org/wiki/OSI_모형](https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95)
- [https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=pst8627&logNo=221670903384](https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=pst8627&logNo=221670903384)
- [https://shlee0882.tistory.com/110](https://shlee0882.tistory.com/110)
- [https://velog.io/@redgem92/네트워크-데이터-링크-계층Data-Link-Layer-1](https://velog.io/@redgem92/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%A7%81%ED%81%AC-%EA%B3%84%EC%B8%B5Data-Link-Layer-1)
- [https://tyeolrik.github.io/network/2017/02/14/Networking-4-Data-Link-Layer.html](https://tyeolrik.github.io/network/2017/02/14/Networking-4-Data-Link-Layer.html)
- [https://movefast.tistory.com/24](https://movefast.tistory.com/24)
