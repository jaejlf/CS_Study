# 💡 시스템 호출 (System Call)

## 1. 정의
시스템 호출(System Call)이란, 운영 체제의 커널이 제공하는 서비스에 대해, 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스를 말한다. 

커널 영역의 기능은 커널 모드에서만 사용할 수 있다. 그런데 일반적인 유저 프로세스는 유저 모드에서 구동되므로 커널의 기능을 직접 사용할 수 없고, 시스템 호출을 인터페이스로 하여 커널의 기능을 사용하여야 한다. 
즉, 프로그래밍 언어에서 지원하는 않는 기능을 사용하기 위해서는 운영체제의 루틴인 시스템 호출을 사용해야 한다.

![](https://velog.velcdn.com/images/wisdom-one/post/2876cfc2-d12f-487f-9b2a-f67ca6e84c97/image.png)

<br/>



## 2. 종류

### 1) 프로세스 제어(process control)
- 끝내기(end), 중지(abort)
- 적재(load), 실행(execute)
- 프로세스 생성(create process)
- 프로세스 속성 획득과 설정(get process attribute and set process attribute)
- 시간 대기(wait time)
- 사건 대기(wait event)
- 사건을 알림(signal event)
- 메모리 할당 및 해제 : malloc, free


### 2) 파일 조작(file manipulation)
- 파일 생성(create file), 파일 삭제(delete file)
- 열기(open), 닫기(close)
- 읽기(read), 쓰기(write), 위치 변경(reposition)
- 파일 속성 획득 및 설정(get file attribute and set file attribute)

### 3) 장치 관리(device management)
- 장치를 요구(request devices), 장치를 방출(release device)
- 읽기, 쓰기, 위치 변경
- 장치 속성 획득, 장치 속성 설정
- 장치의 논리적 부착(attach) 또는 분리(detach)


### 4) 정보 유지(information maintenance)
- 시간과 날짜의 설정과 획득(time)
- 시스템 데이터의 설정과 획득(date)
- 프로세스 파일, 장치 속성의 획득 및 설정


### 5) 통신(communication)
- pipe(), shm_open(), mmap()
- 통신 연결의 생성, 제거
- 메시지의 송신, 수신
- 상태 정보 전달
- 원격 장치의 부착 및 분리


### 6) 보호(Protection)
- chmod()
- umask()
- chown()

<br/>

## 🔖 참고
- https://ko.wikipedia.org/wiki/%EC%8B%9C%EC%8A%A4%ED%85%9C_%ED%98%B8%EC%B6%9C
- https://fjvbn2003.tistory.com/306
- https://dar0m.tistory.com/264

