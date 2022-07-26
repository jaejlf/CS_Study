# 1. 시스템 콜, System Call

> 시스템 콜은 운영체제에게 어떤 기능 수행을 요청하는 수단<br/>
이 기능들은 커널 모드 영역의 기능인데 원칙적으로는 유저 프로세스, 유저 모드에서는 사용하지 못함 → 시스템 콜은 이 기능을 사용자 모드가 사용 가능하게 함 → 프로세스가 하드웨어에 직접 접근하여 필요한 기능을 수행 O
> 

![image](https://user-images.githubusercontent.com/100047095/187927605-9ca14ae4-75cb-4d71-8b5b-629980a06766.png)

출처 : [https://fjvbn2003.tistory.com/306](https://fjvbn2003.tistory.com/306)

<br/>

**특징**

1. 추상화된 하드웨어 인터페이스를 유저 프로세스에게 제공함
2. 시스템의 보안과 안전성을 보장함
3. 가상화된 유저 프로세스와 시스템이 소통할 수 있는 유일하고 공통적인 소통 수단
4. 시스템 호출 시 사용자 → 커널 모드로 변경, 커널에서 시스템 호출 처리를 완료하면 커널 → 사용자 모드로 다시 전환 

![image](https://user-images.githubusercontent.com/100047095/187927631-de1cd01e-2c78-4b9f-8ab8-475f27b81ae5.png)

<br/>

**작동 원리**

1. 사용자  프로세스가 시스템 콜을 요청하면 사용자 → 커널 모드로 전환함 
2. 커널은 각각 시스템 콜을 구분하기 위해 고유 번호를 할당하고 번호에 해당하는 제어 루틴을 커널 내부에 정의함
3. 커널은 요청받은 시스템 콜에 대응하는 번호를 확인함
4. 커널은 그 번호에 맞는 서비스 루틴을 호출함
5. 서비스 루틴을 모두 처리하면 커널 → 사용자 모드로 전환함 

<br/><br/>

# 2. 종류

> 프로세스 제어, 파일 조작, 장치 관리, 정보 유지, 통신
> 

<br/>

**프로세스 제어**

- 끝내기 end, 중지 abort
- 적재 load, 실행 execute
- 프로세스 생성 create process
- 시간 대기 wait time
- 사건 대기 wait event
- 사건 알림 signal event
- 메모리 할당 & 해제 malloc, free

<br/>

**파일 조작**

- 파일 생성 create file
- 파일 삭제  delete file
- 열기 open, 닫기 close
- 읽기 read, 쓰기 write
- 위치 변경 reposition
- 파일 속성 획득 및 설정 get file attribute and set file attribute

<br/>

**장치 관리**

- 장치를 요구 request devices, 장치를 방출 release device
- 읽기, 쓰기, 위치 변경
- 장치 속성 획득, 장치 속성 설정
- 장치의 논리적 부착, 분리

<br/>

**정보 유지**

- time, date
- 시스템 데이터의 설정과 획득
- 프로세스 파일, 장치 속성의 획득 및 설정

<br/>

**통신**

- 통신 연결의 생성, 제거
- 메세지 송신, 수신
- 상태 정보 전달
- 원격 장치의 부착 및 분리

<br/><br/>

# 3. fork()

> fork : 실행 중인 프로세스로부터 새로운 프로세스를 복사하는 함수<br/>
목적 : 빠른 자식 프로세스 실행<br/>
프로세스를 복사할 때 기존의 프로세스는 부모 프로세스가 되고 새로 생긴 프로세스는 자식 프로세스가 됨
>
