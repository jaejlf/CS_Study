암호화와 복호화에 사용하는 암호키가 같은지 다른지에 따라 암호화 기법이 나뉘어 진다.

- 대칭키 암호화 : `암/복호화에 사용하는 키가 동일`한 암호화 방식
- 공개키 암호화 : `암/복호화에 사용하는 키가 서로 다른` 암호화 방식

.
<br>
.

# 📍 대칭키

- 암/복호화키가 동일하기 때문에 해당 키를 아는 사람만이 문서를 복호화해 볼 수 있다
- 대표적인 알고리즘으로는 DES, 3DES, AES, SEED, ARIA 등
- 공개키 암호화 방식에 비해 `속도가 빠르다`는 장점이 있지만, `키를 교환해야한다는 문제`가 발생한다. <br> (키가  탈취될 수도 있고, 사람이 많아질수록 따로따로 키 교환을 해야하기 때문에 관리해야할 키가 방대해진다.)

<br><br>

# 📍 공개키

![image](https://user-images.githubusercontent.com/78673570/190898355-4515cc31-3488-4f9a-9e83-94e969a3e397.png)

- 대칭키의 키 교환 문제를 해결하기 위해 등장한 암호화 방식
- 모든 사람이 접근할 수 있는 `공개키`와, 각 사용자들만이 가지고 있는 `개인키`가 존재한다.
- 공개키는 키가 공개되어있기 때문에 따로 키교환이나 분배를 할 필요가 없다.
- 개인키로만 복호화가 가능하기 때문에 `기밀성`을 제공하며 개인키를 가지고있는 수신자만이 암호화된 데이터를 복호화할 수 있으므로 `일종의 인증기능`도 제공한다.
- 대칭키 방식에 비해 `속도가 느리다`

<br><br>

# 📍 대칭키 vs 공개키

|    | 비밀키 | 공개키
| -- | ----- | ----- 
 키 개수 | 한 개의 키를 사용 | 두 개의 키를 사용
 키 보관 형태 | 비밀리에 보관 | 개인키는 비밀리에, 공개키는 어디든지 배포
 키 교환 | 키를 교환하는 것이 어려우며 위험하다 | 매우 쉽다
 키 길이 | 주로 64 or 128 비트로 짧은 길이 | 주로 512, 1024, 2048 등 긴 길이
 암호화 속도 | 빠르다 | 느리다
 암호화할 수 있는 평문의 길이 | 제한 없음 | 제한 있음
 기밀성 | 가능하다 | 가능하다
 인증 | 부분적으로 가능하다 | 가능하다
 무결성 | 부분적으로 가능하다 | 가능하다
 부인 방지 | 불가능하다 | 가능하다
