# 트랜젝션 격리 수준(Transactiono Isolation Level)

## A. 복습

### (복습) 트랜젝션(Transaction)

데이터의 **정합성**을 보장하기 위한 기능

논리적인 작업 셋 자체가 100%가 보장되거나(COMMIT) 또는 아무것도 적용되지 않아야 함(ROLLBACK)을 보장하는 것

<br/>

### 📚 사전 지식

📌 **[잠금(Lock)](http://www.jidum.com/jidums/view.do?jidumId=283)**

- 트랜잭션이 사용하는 자원 (데이터 항목)에 대하여 상호 배제 (Mutual Exclusive) 기능을 제공하는 기능
- 상호 배제는 특정 트랜잭션이 데이터 항목에 대하여 잠금 (Lock) 을 설정하면, 잠금을 설정한 트랜잭션이 해제 (Unlock) 할 때까지 데이터를 독점적으로 사용할 수 있는 것

📌 **Lock의 유형**

- **공유 잠금(Shared Lock, S Lock)** : Read Lock
- **독점,배타적 잠금(Exclusive Lock, X Lock)** : Write Lock

📌 **2단계 로킹**

- **확장** 단계 : 항목들에 대해 새로운 Lock을 획득 할 수 있지만 해제할 수 없음
- **수축** 단계 : 이미 보유하고 있는 Lock을 해제할 수 있지만 새로운 Lock을 획득 할 수 없음(commit, rollback 등)
- 교착상태는 검출, 시간초과, 방지 프로토콜 등으로 해소

<br/>

## B. 트랜젝션 격리 수준(Transaction Isolation Levels)

동시에 여러 트랜젝션이 처리될 때, 특정 트랜젝션이 다른 트랜젝션에서 변경하거나 조회하는 데이터를 볼 수 있도록 허용할지 결정하는 것.

> 트랜잭션에서 일관성 없는 데이터를 허용하도록 하는 수준

<br/>

트랜젝션이 안정적이게 수행하기 위해 보장해야 할 ACID(원자성, 일관성, 고립성, 지속성)중 **고립성(Isolation)** 에 대하여 성능 관련 문제로 인해 유용하게 조절할 수 있도록 격리 수준을 구분해 놓은 것이다.

<br/>

### 트랜젝션의 격리 수준이 필요한 이유❓

데이터베이스는 ACID 특징과 같이 트랜젝션이 독립적인 수행을 하도록 한다.

따라서 Locking을 통해, 트랜젝션이 DB를 다루는 동안 다른 트랜젝션이 관여하지 못하도록 막는 것이 필요하다.

하지만 무조건 Locking으로 동시에 수행되는 수많은 트랜젝션을 순서대로 처리하게 된다면 데이터베이스의 성능은 떨어지게 된다.

그렇다고 해서 성능을 높이기 위해 Locking의 범위를 줄인다면 **동시성 제어**가 되지 않아 잘못된 값이 처리되는 문제가 발생될수도 있다.

동시성을 증가시키면 데이터 무결성에 문제가 발생하고, 데이터 무결성을 유지하면 동시성이 떨어진다.

<p align="center" style="color:gray">
<img src="https://dataonair.or.kr/publishing/img/knowledge/SQL_280.jpg" height=180>
</p>

→ **따라서 최대한 효율적인 Locking 방법이 필요하다!**

→ DMBS는 다양한 Lock 기법 (Locking, timestamp ordering, MVCC)⁽¹⁾를 활용해 트랜젝션 격리 수준에 맞춰 데이터 접근을 통제한다

→ 아래에서는 **2단계 로킹** 기법을 활용해 설명한다.

<br/>

### 격리 수준의 종류와 발생하는 동시성 제어 문제

<br/>

<p align="center" style="color:gray">
<img width="371" alt="Screen Shot 2022-09-24 at 1 03 13 PM" src="https://user-images.githubusercontent.com/112747890/192079264-54836278-58bc-42f8-a82d-3b636ea10311.png">
</p>

- 격리 수준을 **높일 경우** **성능이 저하**되지만 동시성 제어(Concurrency Control)로 인해 **일관성(Consistency)이 보장됨**
- 격리 수준을 **낮출 경우** **성능은 향상**되지만 동시성 제어(Concurrency Control)에 문제가 생겨 **일관성(Consistency)이 보장되지 않을 수 있음**

<br/>

### 0️⃣ **READ UNCOMMITTED**

- **Isolation Level 0**에 해당하며 기본적인 **갱신 손실(Lost Update)**만 방지하는 상태
- UPDATE와 같이 갱신에 배타적 락을 설정하여 갱신 손실 방지
- 어떤 트랜잭션이 Commit, Rollback 으로 종료되지 않아도 다른 트랜잭션에서 데이터 참조 가능
- SELECT시 공유 락을 설정하거나 체크하지 않기 때문에 다른 트랜잭션이 갱신하면서 설정한 배타적 락을 무시하고 변경 중인 데이터를 참조하거나(**Dirty Read**), 참조중인 데이터를 변경하는 문제(**Unrepeatable Read**), 추가 삽입 되는 데이터 문제(**Phantom Data Read**) 등이 발생

<br/>

### 1️⃣ **READ COMMITED**

- **Isolation Level 1**에 해당하며 Level 0의 기능에 추가로 오손 읽기(**Dirty Read**)까지 방지하는 상태
- SELECT와 같이 읽기에 대하여 공유 락을 설정하여 오손 읽기를 방지
- 단, 공유 락이 트랜잭션이 종료되는 Commit, Rollback 시점까지 유지되는 것이 아닌 SELECT 문이 처리되는 순간만 설정되므로 반복 읽기시 중간에 데이터의 갱신(**Unrepeatable Read**), 삽입(**Phantom Data Read**) 에 의해 문제 발생

<br/>

### 2️⃣ **REPETABLE READ**

- **Isolation Level 2**에 해당하며 Level 1의 기능에 추가로 비반복적 읽기(**Unrepeatable Read**)까지 방지하는 상태
- 공유 락, 배타적 락을 트랜잭션이 종료될 때 까지 유지하여 비반복적 읽기를 방지
- 이 단계부터 Locking 기법을 활용해도 Lock이 많아지고, MVCC 기법을 활용해도 Undo 영역이 커지면서 성능이 떨어 질 수 있음
- 단, SELECT나 UPDATE 등을 이용해 현재 존재하는 데이터에 대해서만 락을 설정하므로 SELECT 등을 이용해 범위 데이터를 처리 할 때 범위 내에 있으나 존재 하지 않아 락이 걸리지 않은 영역에 데이터가 추가로 삽입(**Phantom Data Read**) 되면 문제 발생

<br/>

### 3️⃣ **SERIALIZABLE**

- **Isolation Level 3**에 해당하며 Level 2의 기능에 추가로 유령 데이터 읽기(**Phantom Data Read**)까지 방지하는 상태
- SELECT가 이루어지는 범위(테이블)에 공유락을 설정하여 유령 데이터 읽기를 방지
- 최고 단계 고립 수준으로 일관성이 보장되지만 성능이 안좋음
- 따라서 동시성이 중요한 DB에서는 거의 사용하지 않고 낮은 단계의 격리 수준(일반적으로 READ COMMITED)과 함께 어플리케이션 단계에서 낙관적 락(**Optimistic Lock**), 비관적 락(**Pessimistic Lock**)등을 활용해 처리하는 경우가 많음

#### **MySQL?**

- InnoDB엔진 사용시 Default는 REPEATABLE READ

## 동시성 제어로 발생하는 문제

### 갱신 손실(Lost Update)

<br/>

<p align="center" style="color:gray">
<img width="314" alt="lostUpdate" src="https://user-images.githubusercontent.com/112747890/192079301-b9e55b21-a8ee-40ab-a56f-78174e187fa4.png">
</p>

- 하나의 트랜잭션이 갱신한 내용을 commit/rollback 하기 전에 다른 트랜잭션이 접근해 덮어씀으로서 **갱신 했던 내용이 사라지는** 것을 의미
- **READ UNCOMMITTED** 부터 갱신 손실이 일어나지 않음

<br/>

### 오손 읽기(Dirty Read)

<br/>

<p align="center" style="color:gray">
<img width="302" alt="dirtyRead" src="https://user-images.githubusercontent.com/112747890/192079322-b62257ad-7926-4a0d-ac8f-91eec8e2f836.png">
</p>

- 하나의 트랜잭션이 갱신하려던 내용을 Rollback 하기전에 다른 트랜잭션이 접근해 읽고 처리한 경우 **무효가 된 데이터를 읽는** 것을 의미
- **READ COMMITED**부터 오손 읽기가 일어나지 않음

<br/>

### **비반복적 읽기(Unrepeatable Read)**

<br/>

<p align="center" style="color:gray">
<img width="302" alt="unrepeatableRead" src="https://user-images.githubusercontent.com/112747890/192079356-fdefb841-2d34-498c-a3e6-c76f9170a4d0.png">
</p>

- 하나의 트랜잭션이 **반복적으로 동일한 읽기 연산을 실행** 할 때 다른 트랜잭션의 **갱신완료**로 인해 **이전과 다른 결과**가 나오는 것을 의미
- **REPEATABLE READ**부터 비반복적 읽기가 일어나지 않음

<br/>

### **유령 데이터 읽기(Phantom Data Read)**

<br/>

<p align="center" style="color:gray">
<img width="302" alt="Screen Shot 2022-09-24 at 1 08 30 PM" src="https://user-images.githubusercontent.com/112747890/192079379-d9bd7d9d-61c9-488a-87a0-f29bec9ec6b8.png">
</p>

- 하나의 트랜잭션이 **범위데이터를 읽을 때** 다른 트랜잭션의 데이터 **삽입완료**로 인해 **이전에 없던 유령 데이터가 나타나는** 것을 의미
- **SERIALIZABLE**부터 유령 데이터 읽기가 일어나지 않음

<br/>

### **그 외 문제**

- **모순성(Inconsistency)** : 트랜잭션이 동시에 실행되면서 갱신 전의 값, 갱신 후의 값이 실행 순서에 따라 다르게 읽히면서 데이터가 불일치 하는 문제
- **연쇄복귀(Cascading Rollback)** : 트랜잭선이 동시에 실행되면서 같은 데이터를 공유 할 때 해당 데이터에 대해 한 트랜잭션이 commit을 한 결과에 대해 다른 트랜잭션이 rollback을 할 수 없는 문제

---

1.

- MVCC(Multi-Version Concurrency Control): 하나의 레코드에 대해 여러 버전이 관리된다. 가장 큰 목적은 Lock을 사용하지 않는 일관된 읽기를 제공하는데 있다.
- 타임스탬프: 시스템에서 생성하는 고유 번호인 타임스탬프를 트랜잭션에 부여함으로써 트랜잭션간의 접근 순서를 미리 정한다

2. 낙관적 락과 비관적 락:

- 낙관적 락(Optimistic Lock): 사용자들이 같은 데이터를 동시에 수정하지 않을 것이라고 가정. 데이터를 읽는 시점에 Lock을 걸지 않는 대신 수정 시점에 값이 변경되었는지를 반드시 검사
- 비관적 락(Pessimistic Lock): • 사용자들이 같은 데이터를 동시에 수정할 것이라고 가정. 데이터를 읽는 시점에 Lock을 걸고, 트랜잭션이 완료될 때까지 이를 유지

# C. 참고 자료

🔗 https://github.com/jobhope/TechnicalNote/blob/master/database/IsolationLevel.md
