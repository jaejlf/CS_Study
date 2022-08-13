# 💡 TCP 3-way Handshake

TCP는 장치들 사이에 논리적인 접속을 성립(`establish`)하기 위하여 three-way handshake를 사용한다.

- 양쪽 모두 데이데를 전송할 준비가 되었다는 것을 보장한다.
- 양쪽 모두 상대편에 대한 초기 순차일련변호를 얻을 수 있도록 한다.

<br/>

## 과정

![image](https://user-images.githubusercontent.com/75151848/184482412-0e76f802-a2d1-4f11-85f1-9faab35d17cd.png)

> SYN (synchronize sequence numbers): 연결 확인을 위해 보내는 임의의 숫자값
> 
> ACK (acknowledgment): 전달받은 SYN에 1을 더해 SYN을 잘 받았다는 응답을 보낸다.

<br/>

### 1️⃣ Client > Server : TCP `SYN`

클라이언트는 서버에 접속 요청을 위한 SYN 패킷을 보낸다.

클라이언트는 서버로부터 SYN/ACK 응답을 기다리며, 이 상태가 `SYN_SENT` 상태다.

<br/>

### 2️⃣ Server > Client : TCP `SYN ACK`

서버는 클라이언트의 요청을 수락한다는 의미의 ACK와 SYN flag가 설정된 패킷을 전송한다.

서버는 클라이언트로부터 ACK 응답을 기다리며, 이 상태가 `SYN_RECEIVED` 상태다.

<br/>

### 3️⃣ Client > Server : TCP `ACK`

클라이언트는 서버로 ACK 를 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 된다. 이때 서버의 상태는 `ESTABLISHED` 상태다.

<br/><br/>

# 💡 TCP 4-way Handshake

TCP 4-Way handshake는 세션을 `종료`하기 위해 사용한다.

<br/>

## 과정

![image](https://user-images.githubusercontent.com/75151848/184486854-9693f29d-00da-4d00-a320-599d16bfe936.png)


### 1️⃣ Client > Server : TCP `FIN`

클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송한다.

이때 클라이언트의 상태는 `FIN-WAIT-1` 가 되며, 서버의 `ACK` 와 `FIN` 을 기다린다.

<br/>

### 2️⃣ Server > Client : TCP `ACK`

서버는 확인 메세지를 보내고, 자신의 통신이 끝날 때까지 기다린다.

이때 클라이언트의 상태는 `FIN-WAIT-2` 가 되며, 서버의 `FIN` 을 기다린다.

<br/>

### 3️⃣ Server > Client : TCP `FIN`

서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN 플래그를 전송한다.

<br/>

### 4️⃣ Client > Server : TCP `ACK`

클라이언트가 확인했다는 메세지를 보낸다.

이때 클라이언트는 `TIME-WAIT` 상태가 되며, 혹시 모를 패킷 전송 실패에 대비하여 일정 시간 세션을 유지하다가 종료한다.

<br/>

## Q. 연결 종료를 **3-way Handshake 대신 4-way Handshake로 하는 이유는?**

클라이언트가 데이터 전송을 마쳤다고 하더라도 서버는 아직 보낼 데이터가 남아있을 수 있기 때문이다. 그래서 서버는 일단 FIN에 대한 ACK만 먼저 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내는 것이다.

<br/>

## Q. 클라이언트가 바로 세션을 바로 종료하지 않고 **TIME-WAIT 상태가 되는 이유는?**

클라이언트에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면, 그 패킷은 드롭되고 데이터가 유실된다. 이러한 상황을 대비하기 위해 클라이언트는 서버로부터 FIN을 수신하더라도 일정시간 동안 세션을 남겨놓고 잉여 패킷을 키다리는 과정(TIME-WAIT)을 거친다.

<br/><br/>

## 📌 참고

- [https://mindnet.tistory.com/entry/네트워크-쉽게-이해하기-22편-TCP-3-WayHandshake-4-WayHandshake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)
- [https://sh-safer.tistory.com/146](https://sh-safer.tistory.com/146)
- [https://seongonion.tistory.com/74](https://seongonion.tistory.com/74)
- [https://it-mesung.tistory.com/166](https://it-mesung.tistory.com/166)
