# 💡 SQL vs NoSQL

## SQL 

### 1. 정의

#### RDB (Relational Database)

RDB는 관계형 데이터 모델을 기초로 두고, 모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스를 말한다.

구성된 테이블이 다른 테이블들과 관계를 맺고 모여있는 집합체이며, 테이블간의 관계를 나타내기 위해 외래키(foreign key)를 사용하고 외래키를 이용하여 Join 연산을 할 수 있다.

#### RDBMS (Relational Database Management System)

사용자의 요구에 따라 정보를 생성해 관계형 데이터베이스(RDB)를 생성하고 수정하고 관리할 수 있는 소프트웨어를 말한다.

#### SQL (Structured Query Language)

`RDBMS` 를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어를 말한다.

관계형 데이터베이스 관리 시스템에서 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안되었다.

<br/> 

### 2. ACID
ACID는 다음의 4가지 속성을 뜻하며, RDBMS는 이 속성을 모두 보장한다.
- 원자성(atomicity) : 트랜잭션은 완벽하게 실행하거나 혹은 전혀 실행하지 않는다.
- 일관성(consistency) : 트랜잭션이 커밋되면 데이터가 데이터베이스 스키마를 준수한다.
- 격리성(isolation) : 동시에 일어나는 트랜잭션들이 각기 별도로 실행되어야 한다.
- 내구성(durability) : 예기치 못한 시스템 장애 또는 정전 시 마지막으로 알려진 상태로 복구한다.

<br/> 

### 3. 장단점

#### 장점
- 명확하게 정의된 스키마가 존재하고, 데이터 무결성 보장한다.
- 데이터를 중복 없이 한 번만 저장할 수 있다.

#### 단점
- 스키마로 인해 데이터가 유연하지 못하다. 나중에 스키마를 변경해야 할 경우 번거롭고 어렵다.
- 관계를 맺고 있어서 조인문이 많은 복잡한 쿼리가 만들어질 수 있다.
- 대체로 수직적 확장만 가능하다.

<br/>

> #### 🔖 확장 
> 두 데이터베이스를 비교할 때 중요한 Scaling 개념도 존재한다.
> 데이터베이스 서버의 확장성은 '수직적' 확장과 '수평적' 확장으로 나누어진다.
>
> 수직적 확장 (scale up) : 단순히 데이터베이스 서버의 성능을 향상시키는 것 (ex. CPU 업그레이드)   
> 수평적 확장 (scale out) : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미한다.
>
> 데이터 저장 방식으로 인해 SQL 데이터베이스는 일반적으로 수직적 확장만 지원한다.
> 수평적 확장은 NoSQL 데이터베이스에서만 가능하다.

<br/> 

### 4. 종류

- Oracle (Oracle)
- MS-SQL Server (Microsoft)
- MySQL (Oracle)
- DB2 (IBM)
- Infomix (IBM)
- Sybase (Sybase)
- Derby (APache)
- SQLite (Opensource)

<br/>

## NoSQL

### 1. 정의

NoSQL이란 용어는  사람에 따라 No SQL, Not Only SQL, Non-Relational Operational Database SQL로 엇갈리는 의견들이 있지만 현재 Not Only SQL로 풀어 설명하는 것이 다수를 차지하고 있다.

결국 NoSQL(Not Only SQL)은 기존 관계형 DBMS가 갖고 있는 특성뿐만 아니라, 다른 특성들을 부가적으로 지원한다는 것을 의미한다.

<br/> 

### 2. 특징
- 관계형 모델을 사용하지 않으며 테이블간의 조인 기능이 없다.
- 대부분 여러 대의 데이터베이스 서버를 묶어서(클러스터링) 하나의 데이터베이스를 구성한다.
- 관계형 데이터베이스에서는 지원하는 Data 처리 완결성(Transaction ACID 지원)을 보장하지 않는다.
- 데이터의 스키마와 속성들을 다양하게 수용하고 및 동적 정의가 가능하다. (Schema-less)
- 데이터베이스의 중단 없는 서비스와 자동 복구 기능을 지원한다.
- 다수가 Open Source로 제공된다.
- 확장성, 가용성, 높은 성능

<br/> 

### 3. 장단점

#### 장점
- 스키마가 없어서 유연하다. 언제든지 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장된다. 데이터를 읽어오는 속도 빨라진다.
- 수직 및 수평 확장이 가능하다.

#### 단점
- 데이터가 중복될 수 있으며, 데이터가 변경될 경우 모든 컬렉션의 중복된 데이터를 수정해야 한다.
- 스키마가 존재하지 않기 때문에 명확한 데이터 구조를 보장하지 않고 데이터 구조를 결정하기 어려울 수 있다.

<br/> 

### 4. 종류

- Key Value DB
- Wide Columnar Store
- Document DB
- Graph DB

#### 1) Key Value DB
> Riak, Vodemort, Tokyo 등

`Key와 Value의 쌍`으로 데이터가 저장되는 가장 단순한 형태의 솔루션이다.
Amazon의 Dynamo Paper에서 유래되었다. 


#### 2) Wide Columnar Store
> HBase, Cassandra, ScyllaDB 등

Big Table DB라고도 하며, Google의 BigTable Paper에서 유래되었다. 
Key Value 에서 발전된 형태의 `Column Family` 데이터 모델을 사용하고 있다.


#### 3) Document DB
> MongoDB, CoughDB 등

Lotus Notes에서 유래되었으며, JSON, XML과 같은 `Collection` 데이터 모델 구조를 채택하고 있다. 

#### 4) Graph DB
> Neo4J, OrientDB 등

Euler & Graph Theory에서 유래되었으며 `Nodes`, `Relationship`, `Key-Value` 데이터 모델을 채용하고 있다. 

<br/>

## 정리 
### SQL 데이터베이스 사용이 더 좋은 경우

- 관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션의 경우
- NoSQL에서는 여러 컬렉션을 모두 수정해야 하기 때문에 비효율적
- 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우


### NoSQL 데이터베이스 사용이 더 좋을 경우

- 정확한 데이터 구조를 알 수 없거나 변경/확장 될 수 있는 경우
- 읽기를 자주 하지만, 데이터 변경은 자주 없는 경우
- 데이터베이스를 수평으로 확장해야 하는 경우 (막대한 양의 데이터를 다뤄야 하는 경우)

<br/><br/> 

## 🔖 참고
- https://im-designloper.tistory.com/67
- https://ourcstory.tistory.com/30
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/SQL%EA%B3%BC%20NOSQL%EC%9D%98%20%EC%B0%A8%EC%9D%B4.md
- https://www.samsungsds.com/kr/insights/1232564_4627.html
