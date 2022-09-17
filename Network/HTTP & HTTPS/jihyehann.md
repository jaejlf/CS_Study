# 💡 HTTP & HTTPS

## 1. HTTP (Hyper Text Transfer Protocol)

### 1) 정의

HTTP는 `서버/클라이언트` 모델을 따라 데이터를 주고 받기 위한 프로토콜이다.

인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, `80번` 포트를 사용한다.

1989년 팀 버너스 리(Tim Berners Lee)에 의해 처음 설계되었다.

<br/>

###  2) 구조

HTTP는 애플리케이션 레벨의 프로토콜로 `TCP/IP` 위에서 작동한다. 

HTTP는 상태를 가지고 있지 않는 Stateless 프로토콜이며 `Method`, `Path`, `Version`, `Headers`, `Body` 등으로 구성된다.

![image](https://user-images.githubusercontent.com/75151848/190839781-aaf20685-35de-4e61-90b8-476420f3188b.png)

<br/><br/>

## 2. HTTPS (Hyper Text Transfer Protocol Secure)

### 1) 정의

HTTPS는 HTTP에 데이터 `암호화`가 추가된 프로토콜이다.

`443번` 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원하고 있다.

<br/>

### 2) 암호화

HTTPS는 `대칭키 암호화`와 `비대칭키 암호화`를 모두 사용하여 빠른 연산 속도와 안정성을 모두 가진다.

<br/>

#### 비대칭키 암호화 사용

HTTPS의 연결 과정(handshake)에서 서버와 클라이언트 간에 `세션키`를 교환한다.

이때 `비대칭키`를 사용하여, 안전하게 세션키를 공유한다. 

> 🔖 HTTPS의 HandShake에 관한 자세한 내용은 [여기](https://github.com/jaejlf/CS_Study/blob/main/Network/TLS%20%26%20SSL%20handshake/jihyehann.md)를 참고

<br/>

#### 대칭키 암호화 사용

handshake 과정에서 교환한 세션키는 이후 데이터를 주고받을 때 암호화를 위해 `대칭키`로 사용된다. 

여기서 대칭키를 사용하는 이유는 데이터 교환 시의 빠른 연산 속도를 위해서다.

<br/>

### 3) 비대칭키 발급 과정

서버는 클라이언트와 세션키를 공유하기 위한 공개키를 생성해야 하는데, 일반적으로는 인증된 기관(Certificate Authority)에 공개키를 전송하여 인증서를 발급받는다. 

1. 서버는 HTTP 기반의 애플리케이션에 HTTPS를 적용하기 위해 공개키/개인키를 발급한다.
2. 서버는 CA(Certificate Authority)에 돈을 지불하고, 공개키를 저장하는 인증서의 발급을 요청한다.
3. CA는 CA 기업의 이름, 서버의 공개키, 서버의 정보 등을 기반으로 인증서를 생성하고, CA의 개인키로 암호화하여 서버에게 인증서를 제공한다.
4. 서버는 클라이언트에게 암호화된 인증서를 제공한다.
5. 클라이언트(브라우저)는 CA의 공개키를 미리 다운받아 갖고 있고, 이 공개키를 이용해 암호화된 인증서를 복호화한다.
6. 클라이언트는 암호화된 인증서를 복호화하여 얻은 서버의 공개키로 세션키를 공유한다.


<br/><br/>

## 3. HTTP vs HTTPS
### 1) 보안
HTTP는 암호화가 추가되지 않았기 때문에 보안에 취약하다.

반면, HTTPS는 안전하게 데이터를 주고받을 수 있다. 

<br/>

### 2) 속도
HTTPS는 암호화/복호화의 과정이 필요하기 때문에 HTTP보다 속도가 느리다. 

(물론 오늘날에는 거의 차이를 못 느낄 정도이다.) 

<br/>

### 3) 비용
HTTPS는 인증서를 발급하고 유지하기 위한 추가 비용이 발생하다.

<br/>

### 결론

**개인정보와 같은 민감한 데이터를 주고 받아야 한다면 HTTPS를 이용하고, 노출되어도 괜찮은 단순한 정보 조회 등 만을 처리하고 있다면 HTTP를 이용하자.**

<br/>

## 🔖 참고
- [[Web] HTTP와 HTTPS의 개념 및 차이점](https://mangkyu.tistory.com/98)