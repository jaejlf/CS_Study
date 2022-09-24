# 💡 트랜잭션 격리 수준(Transaction Isolation Level)	

트랜잭션 격리수준(isolation level)이란 "동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 서로 고립되어 있는지"를 나타내는 것이다.

즉, 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를 볼 수 있도록 허용할지를 결정하는 것이다.

격리수준은 크게 아래의 4개로 나뉜다.

- Read Uncommitted
- Read Committed
- Repeatable Read
- Serializable

아래로 내려갈수록 트랜잭션 간 고립 정도가 높아지며, 성능이 떨어지는 것이 일반적이다.

일반적인 온라인 서비스에서는 `Read Committed`나 `Repeatable Read` 중 하나를 사용한다. <br/>
(oracle = Read Committed, mysql = Repeatable Read)

 <br/>

### 트랜잭션 격리 수준이 필요한 이유 

`트랜잭션 수준 읽기 일관성` (Transaction-Level Read Consistency)을 지키기 위해서이다.
- 트랜잭션 수준 읽기 일관성이란, 트랜잭션이 시작된 시점으로부터 일관성 있게 데이터를 읽어들이는 것을 말한다.
- 하나의 트랜잭션이 진행되는 동안 다른 트랜잭션에 의해 변경사항이 발생하더라도 이를 무시하고 계속 일관성 있는 데이터를 보여준다. <br/>
(물론 트랜잭션 자신이 발생한 변경사항은 읽을 수 있다)

<br/>

## 1. 트랜잭션 격리수준 유형

### 1) Read Uncommitted (레벨 0)

<img width="60%"
     src="https://user-images.githubusercontent.com/75151848/192092934-8a620050-35c9-4fd2-bc91-12830e09ebe8.png"/>

- SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리지 않는 계층.
- 트랜잭션에 처리중이거나, 아직 Commit되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용한다.
- 데이터베이스의 일관성을 유지하는 것이 불가능하다.
- Dirty Read, Non-Repeatable Read, Phantom Read 현상이 발생한다.

<br/>

### 2) Read Committed (레벨 1)

<img width="60%"
     src="https://user-images.githubusercontent.com/75151848/192093078-c3cfc37e-2e81-42bc-a031-5da7c03bb2c6.png"/>

- SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리는 계층. 
- 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 된다.
- Commit이 이루어진 트랜잭션만 조회 가능하다.
- 대부분의 SQL 서버가 Default로 사용하는 Isolation Level이다.
  -  DB2, SQL Server, Sybase의 경우 읽기, 공유 Lock을 이용하여 구현한다.
  - Oracle은 Lock을 사용하지 않고 쿼리시작 시점의 Undo 데이터를 제공한다.
- Dirty Read 가 발생하지 않지만 Non-Repeatable Read, Phantom Read 현상은 여전히 발생한다.

<br/>

### 3) Repeatable Read (레벨 2)

<img width="60%"
     src="https://user-images.githubusercontent.com/75151848/192093153-e58d44a4-7ba6-43f0-838f-9d45050db855.png"/>

- 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층.
- 트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일함을 보장한다.
- 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정이 불가능하다.
- MySQL에서 Default로 사용하는 Isolation Level으로, MySQL에서는 트랜잭션마다 트랜잭션 ID를 부여하여 트랜잭션 ID보다 작은 트랜잭션 번호에서 변경한 것만 읽게 된다.
- 변경되기 전 레코드는 Undo 공간에 백업해두고 실제 레코드 값을 변경한다.
- Dirty Read와 같은 현상은 발생하지 않지만 Phantom Read 현상은 여전히 발생한다.

<br/>

### 4) Serializable (레벨 3)

- 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층.
- 완벽한 읽기 일관성 모드를 제공한다.
- 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능하다.
- 가장 엄격한 격리 수준으로 Phantom Read가 발생하지 않는다.

<br/>

## 2. 격리수준 비교

![image](https://user-images.githubusercontent.com/75151848/192093246-5132276c-dcfd-46d1-a534-5a388ecfb327.png)

### 1) Dirty Read (Uncommitted Dependency)

- 커밋되지 않은 수정중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상.
- 변경 후 아직 Commit 되지 않은 값을 읽고, Rollback 후의 값을 다시 읽어 최종 결과 값이 상이한 현상이다.

### 2) Non-Repeatable Read (Inconsistent Analysis)

- 한 트랜잭션 내에서 같은 쿼리를 두 번 수행할 때, 그 사이에 다른 트랜잭션이 값을 수정 또는 삭제함으로써 두 쿼리가 상이하게 나타나는 일관성이 깨진 현상.

### 3) Phantom Read

- 하나의 트랜잭션에서 같은 쿼리를 두 번 실행했을 경우, 첫 번째 쿼리에서 없던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상이다.
- 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타나는 현상이다.

<br/><br/>

> #### 🔖 참고
> - [트랜잭션 격리 수준(Transaction Isolation Level)
](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md)
> - [[데이터베이스] 트랜잭션 격리수준](https://velog.io/@guswns3371/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC%EC%88%98%EC%A4%80)
