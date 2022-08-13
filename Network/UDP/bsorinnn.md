# UDP

## A. UDP란?

- UDP(User Datagram Protocol)는 `비연결형`, `신뢰성이 없는` 전송 프로토콜
- IP데이터그램을 캡슐화하여 보내는 방법과 연결 설정을 하지 않고 보내는 방법을 제공
- TCP/IP 5계층에서 Transport Layer(전송계층)의 프로토콜

## B. UDP의 특징

- 흐름 제어, 오류 제어 또는 손상된 세그먼트의 수신에 대한 재전송이 없다
- 따라서 내용이 전송 중 손실될 수 있고, 전송되는 세그먼트의 순서가 바뀔 수도 있다.
- UDP는 TCP보다 간단하고 빠르다
- 작은 Header size를 가지고 있다.
- 흐름제어를 하지 않기 떄문에 전송 속도로르 최대한 빠르게 할 수 있다.
- 수신자와 송신자 간 handshaking이 없는 connectionless 성질을 가진다
- 1:1, 1:다(Broadcast), 다:다 (MultiCast) 통신을 수행

## C. UDP 사용하는 이유

TCP와 다르게 흐름제어나 오류 제어가 없기 때문에 전송 속도를 빠르게 할 수 있으나 TCP처럼 신뢰성 있는 전송을 보장할 수 없다.<br>
=> 신뢰성보다 **속도**가 중요한 부문에서 UDP 사용

ex) 스트리밍, DNS, SNMP

## D. 표로 비교하는 TCP와 UCP

| TCP                                                          | UDP                                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------- |
| Connection-oriented Protocol(연결 지향형 프로토콜)           | Connection-less protocol(비 연결지향형 프로토콜)              |
| Connection by **byte** stream(바이트 스트림을 통한 연결)     | Connection by **message** stream(메세지 스트림을 통한 연결)   |
| Congestion / Flow control(혼잡제어, 흐름제어)                | NO Congestion / Flow control(혼잡제어와 흐름제어 지원 X)      |
| Ordered, Lower speed(순서 보장, 상대적으로 느림)             | Not ordered, Higer speed(순서 보장되지 않음, 상대적으로 빠름) |
| Reliable data transmission(신뢰성 있는 데이터 전송 - 안정적) | Unreliable data transmission(데이터 전송 보장 X)              |
| TCP packet : Segment(세그먼트 TCP 패킷)                      | UDP packet : Datagram(데이터그램 UDP 패킷)                    |
| HTTP, Email, File transfer에서 사용                          | DNS, Broadcasting(도메인, 실시간 동영상 서비스에서 사용)      |

## E. UDP의 헤더

<img src="https://cheapsslsecurity.com/blog/wp-content/uploads/2022/06/udp-header.png" height=150>

- UDP 헤더는 다음과 같이 8 Byte로 **고정**되어 있다.

( N 바이트 )

- 출발지 포트(2), 도착지 포트(2)
- 전체 길이(2)
  - **헤더와 데이터 전체**의 총 길이
- 체크섬(2)
  - 데이터의 변조를 확인하기 위한 값, 보낸 값과 받은 값을 비교

## F. 참고자료

🔗 https://code-lab1.tistory.com/25

🔗 https://velog.io/@hidaehyunlee/TCP-와-UDP-의-차이
