# 1. Blocking I/O

I/O 작업은 유저레벨에서 수행할 수 없고 커널레벨에서만 가능함. 따라서 유저 프로세스는 커널에게 I/O를 요청해야 함. Blocking I/O는 유저 프로세스가 커널에게 I/O를 요청하는 함수를 호출하고 커널이 작업을 완료하면 함수가 작업 결과를 반환하는 형태임. 

![image](https://user-images.githubusercontent.com/100047095/196027687-af238bc4-65e8-41d9-8246-724d3eeed7bc.png)

<br/>

위 사진과 같이 I/O 작업이 진행되는 동안 유저 프로세스는 자신의 작업을 중단한 채 기다려야 함. I/O 작업이 CPU 자원을 거의 사용하지 않으므로 Blocking I/O는 자원 낭비가 심함. 

여러 클라이언트가 접속하는 서버를 블로킹 방식으로 구현한다고 가정햇을 때, I/O를 하나의 클라이언트에서 진행하면 해당 클라이언트의 프로세스나 쓰레드가 진행하는 작업을 중단하게 됨. → 다른 클라이언트의 작업에 영향을 미치지 않게 하기 위해 클라이언트 별로 별도의 쓰레드를 만들어 연결시켜주어야 하므로 많은 쓰레드가 만들어지게 됨 → 컨텍스트 스위칭이 많이 일어나므로 리소스 낭비 심함. 

<br/><br/>

# 2. Non-Blocking I/O

I/O 작업을 진행하는 동안 유저 프로세스의 작업을 중단하지 않음. 유저 프로세스가 커널에게 I/O를 요청하는 함수를 호출하면 함수는 I/O를 요청한 다음 진행상황과 상관 없이 바로 결과를 반환함. 

![image](https://user-images.githubusercontent.com/100047095/196027683-92fc78a5-d0a6-4af1-b1e7-b9d99961ce46.png)

<br/>

**과정**

1. 유저 프로세스는 `recvfrom` 함수를 호출하여 커널에게 해당 소켓으로부터 데이터를 받고 싶다고 요청함
2. 커널은 이 요청에 대해서 상대방의 데이터를 전송 받아 `recvBuffer`에 저장하고 유저에게 그 내용을 복사해주어야 함. 상대방으로부터 데이터를 받는 중에 이 버퍼가 비어있다면 유저 프로세스가 커널에게 받아올 정보는 없음. → `recvfrom` 함수가 진행중이라는 의미로 `EWOULDBLOCK`을 리턴함. 
3. 이 값을 리턴받은 유저 프로세스는 다른 작업을 진행할 수 있음. 
4. 버퍼에 값이 있어 유저 프로세스가 받을 데이터가 있다면 버퍼로부터 데이터를 복사하여 받아옴.
