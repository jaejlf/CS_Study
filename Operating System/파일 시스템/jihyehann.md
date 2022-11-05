# 💡 파일 시스템(File System)

## 1. 파일 (File)

파일이란 저장 장치에 연관된 정보의 `논리적 저장 단위` 이다.

물리적으로는 바이트의 나열(Sequence of Bytes)로 볼 수 있다.

- 파일 속성 : 파일 이름, 유형, 위치, 크기, 소유자, 제어 정보, 만들어진 시간 등이 있다. 
- 파일 연산 : 생성(Create), 삭제(Delete), 열기(Open), 닫기(Close), 읽기(Read), 쓰기(Write) 등
- 파일의 구성 방식에 따른 분류 : 더미 파일, 순차 파일, 인덱스 파일, 인덱스 순차 파일, 직접 파일 

<br/>

## 2. 파일 시스템 (File System)

- 컴퓨터에서 파일이나 자료를 쉽게 발견할 수 있도록, 유지 및 관리하는 방법
- 저장매체에는 수많은 파일이 있기 때문에, 이런 파일들을 관리하는 방법

### 특징

- 커널 영역에서 동작한다.
- 파일 CRUD 기능을 원활히 수행하는 것을 목적으로 한다.
- 계층적 디렉터리 구조를 가진다.
- 디스크 파티션 별로 하나씩 둘 수 있다.

### 역할

- 파일 관리
- 보조 저장소 관리
- 파일 무결성 메커니즘
- 접근 방법 제공

### 개발 목적

- 하드디스크와 메인 메모리 속도차를 줄이기 위해
- 파일 관리를 위해
- 하드디스크 용량 효율적으로 이용하기 위해

<br/>

## 3. 파일 접근 방법

### 1) 순차 접근 (Sequential Access) (순차 파일)

가장 간단한 접근 방법으로, 대부분 연산은 read와 write이다.

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/d19e8026-fbed-4720-9d05-ab81b597fdc7/image.png"/>

- 현재 위치를 가리키는 포인터에서 시스템 콜이 발생할 경우 포인터를 앞으로 보내면서 read와 write를 진행한다.
- 뒤로 돌아갈 땐 지정한 offset만큼 되감기를 해야 한다. (테이프 모델 기반)

<br/>

### 2) 직접 접근 (Direct Access) (직접 파일)

특별한 순서없이, 빠르게 레코드를 read, write 가능하다.

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/3b1157c6-7a40-4043-bf6c-ed56389a053a/image.png"/>

- 현재 위치를 가리키는 cp(current position) 변수만 유지하면 직접 접근 파일을 가지고 순차 파일 기능을 쉽게 구현이 가능하다.
- 무작위 파일 블록에 대한 임의 접근을 허용한다. 따라서 순서의 제약이 없다.
- 대규모 정보를 접근할 때 유용하기 때문에 '데이터베이스'에 활용된다.

<br/>

### 3) 기타 접근 (인덱스 파일)

직접 접근 파일에 기반하여 색인을 구축한 방법

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/b47d2231-a3c9-49eb-8e1d-1782370510d3/image.png"/>


<br/>

## 4. 파일 시스템의 구조

### 1) 1단계 디렉터리 구조

- 가장 간단한 구조
- 파일 시스템 전체에 한 개의 디렉터리가 존재하고, 모든 파일들은 이 디렉터리 내에 저장된다.
- 디렉터리 내의 파일들은 서로 다른 유일한 이름을 가져야한다. (다중 사용자 시스템에서 문제가 될 수 있음)

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/5eacffcb-6c2b-419b-8295-f73f382c4e30/image.png"/>

<br/>

### 2) 2단계 디렉터리 구조

- 사용자당 하나의 디렉터리 구조를 갖는 구조 (1단계 디렉터리 구조의 문제의 해결)
- 사용자는 하부 디렉터리를 가질 수 없다. (2단계로만 구성 가능)

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/a0fc660e-0d28-426a-9674-9396b1aded3a/image.png"/>

- MFD : 사용자의 이름과 계정번호로 색인되어 있는 디렉터리
- UFD : 자신만의 사용자 파일 디렉터리

<br/>

### 3) 트리(계층) 디렉터리 구조

- 2단계 구조 확장된 다단계 트리 구조
- 1 bit를 이용하여, 일반 파일(0)인지 디렉터리 파일(1) 구분한다.
- 루트 디렉터리 : 최상위 디렉터리
- 시스템 내의 모든 파일들은 고유한 경로(path)명을 가진다.

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/3f39c212-24dd-4bb6-83be-10086548ef05/image.png"/>

<br/>

### 4) 그래프 디렉터리 구조

- 계층구조에서 링크를 통해 임의의 디렉터리를 다른 디렉터리와 연결시켜 서로 같이 사용할 수 있도록 하는 구조.
- 즉, 사용자들이 각자의 위치에서 링크를 거쳐 동일한 디렉터리나 파일로 접근할 수 있도록 만들어진 구조.
- 사이클이 발생하지 않도록, 하위 디렉터리가 아닌 파일에 대한 링크만 허용하거나, 가비지 컬렉션을 이용해 전체 파일 시스템을 순회하고 접근 가능한 모든 것을 표시한다.

<img width="70%"
     src="https://velog.velcdn.com/images/wisdom-one/post/84ed26da-1da2-4119-a316-353fa3c75765/image.png"/>


<br/><br/>

[참고](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/File%20System.md)
