# 💡 Race Condition (경쟁 상태)

## Race Condition 이란?  
두 개 이상의 cocurrent한 프로세스(혹은 스레드)들이 하나의 자원(리소스)에 접근하기 위해 경쟁하는 상태. 

공용 데이터에 대한 접근이 어떤 순서에 따라 이루어졌는지에 따라 그 실행 결과가 같지 않고 달라지게 된다.

이러한 경쟁 프로세스들로 인해, `상호배제 (Mutual exclusion)` , `교착 상태 (Deadlock)` , `기아 (Starvation)` 과 같은 문제가 발생하게 된다.

<br/>

## 상호배제 (Mutual exclusion)

두 개 이상의 프로세스가 동시에 사용할 수 없는 자원을 `임계자원 (Critical Resource)` 이라고 부르며, 이러한 자원에 대해 접근하고 실행하는 프로그램 내의 코드 부분을 `임계영역 (Critical Section)` 이라고 한다.

`상호배제` 란, 한 번에 하나의 프로세스만이 임계영역에 들어가야 함을 의미한다.

**임계영역의 성공적인 실행을 위해서는 가장 먼저 상호배제가 지켜져야 한다.**

상호배제의 원칙은 다음과 같다.

- 임계영역에 있지 않는 프로세스가 다른 프로세스의 임계영역 진입을 막아서는 안 된다. 
- 비어있는 임계영역에 대한 진입은 바로 허용한다. 
- 특정 프로세스의 진입 시도가 계속 무산되어 기아를 겪지 않도록 해야 한다.

임계영역에 들어가고자 하는 프로세스는 먼저 임계영역 내 다른 프로세스가 있는지를 확인한 후 있다면 기다리고, 없다면 들어가면서 자신이 나올 때까지 다른 프로세스가 들어오지 못하도록 해야 한다.  
또한, 임계영역을 벗어날 때는 자신이 나오는 사실을 알려 다른 프로세스가 들어올 수 있도록 해야한다.

<br/>

## 교착 상태 (Deadlock)

그러나 상호배제를 시행하면 교착 상태 (Deadlock)가 발생할 수 있다.

교착 상태란 둘 이상의 프로세스들이 자원을 점유한 상태에서 서로 다른 프로세스가 점유하고 있는 자원을 요구하며 무한정 기다리는 현상을 말하며, 교착 상태의 발생 조건 중 하나가 상호배제다.

> 🔖 자세한 내용은 [이전 정리](https://github.com/jaejlf/CS_Study/blob/main/Operating%20System/%EB%8D%B0%EB%93%9C%EB%9D%BD(DeadLock)/jihyehann.md)를 참고하자.

<br/>

## 기아 (Starvation)

기아 상태란 특정 프로세스가 원하는 자원을 계속 할당받지 못하는 상태를 말한다.

기아 상태는 여러 프로세스가 부족한 자원을 점유하기 위해 경쟁할 때 발생하게 된다. 
스케줄링이나 상호배제 알고리즘의 오류 혹은 자원 누수나 고의적인 서비스 거부 공격으로 인해 발생할 수도 있다.

<br/><br/>


## 🔖 참고
- [블로그](https://iredays.tistory.com/125)

