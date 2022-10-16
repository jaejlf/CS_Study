# 💡 Blocking & Non-Blocking I/O


## I/O 

I/O(Input/Output) 작업은 Kernel level에서만 수행할 수 있다. 

따라서 User level의 Process나 Thread는 반드시 커널에게 I/O를 요청해야 한다.

커널에게 I/O 요청 시, 결과를 반환받을 때까지 프로세스의 작업을 중단시키느냐에 따라 Blocking I/O과 Non-Blocking I/O으로 나눌 수 있다.

<br/>

## Blocking I/O

I/O 작업이 진행되는 동안 User 프로세스는 자신의 작업을 중단한 채 대기하는 방식.

가장 기본적인 I/O 모델로, linux에서 모든 소켓 통신은 기본 blocking으로 동작한다.

![](https://velog.velcdn.com/images/wisdom-one/post/73fe1e6e-528e-437a-9cca-2c5efc6639e5/image.png)

1. 프로세스는 커널에게 read 작업 요청
2. 데이터가 입력될 때까지 대기
3. 데이터가 입력된 후 결과가 프로세스에게 전달되면, 프로세스 작업으로 복귀

이 방식은 입출력 요청 시, 애플리케이션이 다른 작업을 수행하지 못하고 기다리게 되므로 자원이 낭비될 수 있다.

또한, 여러 Client 가 접속하는 서버를 Blocking 방식으로 구현하게 되면, I/O 작업을 진행하는 작업을 중지할 때 다른 Client가 진행중인 작업을 중지하면 안되므로, client 별로 별도의 Thread를 생성해야 하기 때문에 많아진 Threads 로 컨텍스트 스위칭 횟수가 증가하게 된다는 문제가 있다.

<br/>


## Non-Blocking I/O

I/O 작업이 진행되는 동안 User 프로세스의 작업을 중단시키지 않는 방식.

![](https://velog.velcdn.com/images/wisdom-one/post/916039a4-93f0-45b6-8fd6-053b568b780c/image.png)

1. 유저 프로세스가 커널에게 read 작업 요청하기 위해 
recvfrom 함수 호출
2. recvfrom 함수를 통해 바로 결과를 반환받음. <br/>
이때, 입력 데이터가 없으면 입력 데이터가 없다는 결과 메세지(`EWOULDBLOCK`)를 반환받음.
3. 입력 데이터가 있을 때까지 1-2번 반복 (입력 데이터가 없는 경우, 유저 프로세스는 다른 작업을 수행할 수 있음)
4. 입력 데이터가 있으면, recvfrom 함수가 빠른 속도로 data를 복사한 후, 복사한 data의 길이와 함께 프로세스에게 반환

<br/>


## 🔖 참고
- [gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/%5BNetwork%5D%20Blocking%20Non-Blocking%20IO.md)
- [블로그](https://ju3un.github.io/network-basic-1/)

