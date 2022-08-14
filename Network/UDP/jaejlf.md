cf. 데이터의 전달을 담당하는 `전송 계층(Transport Layer)`에서 `TCP`, `UDP` 표준을 사용한다.

<br>

# 📍 TCP (Transmission Control Protocol)

![image](https://user-images.githubusercontent.com/78673570/184525180-2c0ecd2d-7cdd-44e7-83e6-3c5832142b1e.png)

1. SYN 데이터 전송 : 클라이언트가 연결 요청
2. SYN ACK : 서버가 연결 수락 (만약 ACK를 수신하지 못하면 재전송) 
3. 통신 선로 고정

<br>

=> 모든 데이터는 `고정된 통신 선로`를 통해 `순차적으로 전달`된다.

<br>

=> 연속성보다 신뢰성 있는 전송이 중요할 때 사용하는 프로토콜 (ex. 메일 전송, 파일 전송)

<br>

## TCP 헤더

![image](https://user-images.githubusercontent.com/78673570/184525990-74834051-db17-4c65-9e56-0a3c5728291a.png)

- `Source Port` : 데이터를 생성한 애플리케이션에서 사용하는 포트 번호
- `Destination Port` : 목적지 애플리케이션이 사용하는 포트 번호 (ex. HTTP - 80, SMTP - 25)
- `Sequence Number` : 전송하는 데이터의 순서 보장을 위한 번호
- `Acknowledgement Number` : 승인 번호, 데이터를 받은 수신자가 예상하는 다음 시퀀스 번호
- `Data Offset` : 헤더가 아닌 실제 데이터가 시작되는 위치 표시
- `Reserved` : 나중에 사용하기 위해 예약된 필드 (현재 사용 X, 모두 0으로 채워져있다.)
- `TCP Flags` : 제어 플래그
   - **CWR(Congestion Window Reduced)** : 혼잡 윈도우 크기 감소
   - **ECN(Explicit Congestion Notification)** : 혼잡을 알림
   - **URG(Urgent)** : 긴급 비트, Urgent Pointer 필드가 가리키는 세그먼트 번호까지 우선 순위가 높은 긴급 데이터가 포함되어있다는 것
   - **ACK(Acknowledgment)** : 승인 비트, 확인 응답 메세지
   - **PSH(Push)** : 밀어넣기 비트
   - **RST(Reset)** : 초기화 비트, 상대방과 연결되어 있는 상태에서 어떠한 문제가 발생하여 수신을 거부하고 연결 상태를 리셋
   - **SYN(Synchronize)** : 동기화 비트, 연결이 시작될 때 무조건 사용되는 플래그
   - **FIN(Finish)** : 종료 비트, 작업이 끝나고 가상 회선을 종결하고자 할 때 사용
- `CheckSum` : 오류 감지를 위한 값
- `Urgent Pointer` : 긴급 포인터, URG 플래그가 1이면 수신측은 이 포인터가 가리키고 있는 데이터를 우선 처리

<br>

## 특징

- `양방향 연결(Full Duplex Connection)`형 서비스 제공
- `가상 회선 연결(Virtual Circuit Connection)` 형태의 서비스 제공
- `Connection` 연결 : [3-way/4-way handshaking](https://github.com/jaejlf/CS-Study/blob/main/Network/TCP%20handshake/jaejlf.md)
- `신뢰성 있는` 경로를 확립하고 메세지 전송을 감독
- 데이터의 `전송 순서를 보장` : 데이터의 순서 유지를 위해 각 바이트마다 번호 부여
- `흐름 제어`, `혼잡 제어`, `오류 감지`
- 스트림 위주의 전달(`패킷 단위`)
- 패킷의 분실/손상/지연이나 순서가 틀렸을 경우 `투명성이 보장`되는 통신을 제공
- UDP보다 `전송 속도가 느리다`

<br><br>

# 📍 UDP (User Datagram Protocol)

![image](https://user-images.githubusercontent.com/78673570/184525302-cbab13ae-2ff0-42d8-b917-c0c667a27b31.png)

- 통신 선로를 고정하지 않기 때문에, 발신자가 데이터 패킷을 순차적으로 보내더라도 서로 다른 통신 선로를 통해 전달될 수 있다. 즉, `전송 순서가 보장되지 않는다`
- 중간에 패킷이 유실/변조되더라도 `재전송을 하지 않는다`

<br>

## 특징

- 데이터 전송 전에 연결을 설정하지 않는 `비연결형(Connectionless)` 서비스 제공
- TCP에 비해 상대적으로 `단순한 헤더 구조`를 가지므로, `오버헤드가 적다`
- `오류 감지` (흐름 제어, 혼잡 제어를 하지 않기 때문에 `전송 속도가 빠르다`)
- `실시간 전송에 유리`


<br>

=> 신뢰성보다는 속도가 중요시되는 네트워크에서 사용하는 프로토콜 (ex. 영상 스트리밍)

<br>

# 📍 정리

### 공통점

- `포트 번호`를 이용해 주소를 지정한다.
- `오류 감지` 기능을 제공한다.

<br>

### 차이점

프로토콜 | TCP | UDP
 -- | -- | --
 연결 방식 | 연결형 | 비연결형
 패킷 교환 방식 | 가상 회선 방식 | 데이터그램 방식
 전송 순서 | 전송 순서 보장 | 전송 순서가 바뀔 수 있음
 수신 여부 확인 | O | X
 통신 방식 | 1:1 통신 | 1:1 or 1:N or N:N
 신뢰성 | 높다 | 낮다
 속도 | 느리다 | 빠르다
