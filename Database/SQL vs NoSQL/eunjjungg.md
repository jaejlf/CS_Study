# 1. SQL

> RDBMS에서 데이터를 저장, 수정, 삭제 및 검색할 수 있음
> 

<br/>

**특징**

- 데이터는 정해진 데이터 스키마에 따라 테이블에 저장됨
- 데이터는 관계를 통해 여러 테이블에 분산됨

<br/>

관계형 데이터베이스의 데이터는 정해진 schema를 따라 데이터베이스 테이블에 저장됨

→ schema를 준수하지 않은 Row는 추가할 수 없음 

관계를 통해 연결된 여러 개의 테이블에 데이터가 분산됨

![image](https://user-images.githubusercontent.com/100047095/185764162-cee9f312-f9a3-4ce3-a293-210077f88cf2.png)

<br/>

**관계**

데이터들을 여러 개의 테이블에 나눠서 저장하기에 데이터의 중복을 피할 수 있음

하지만 중복 없이 각 테이블이 하나의 데이터만을 관리하기에 다른 테이블에서 부정확한 데이터를 다룰 수 있다는 위험이 존재

<br/><br/>

# 2. NoSQL

<br/>

**종류**

- 키-값 DB : redis, riak
- 도큐먼트 DB : mongoDB, couchDB
- 컬럼 패밀리 DB : cassandra, hbase
- 그래프 DB : neo4j, orientDB

<br/>

**특징**

- 유연성 : schema 선언 없이 필드의 추가, 삭제가 자유로움
- 확장성 : 스케일 아웃에 의한 서버 확장이 용이함
- 고성능 : 대용량 데이터를 처리하는 성능이 뛰어남
- 가용성 : 여러 대의 백업 서버 구성이 가능하며 장애 발생 시에도 무중단 서비스가 가능

<br/>

**document DB**

레코드를 document라고 부름

NoSQL은 다른 구조의 데이터를 같은 컬렉션에 추가가 가능함 (SQL에서는 스키마를 따르지 않으면 데이터 추가가 불가능했음) 

주문 관련 정보를 SQL에서는 Orders, Users, Products 테이블로 나눴지만 NoSQL에서는 Orders에 한꺼번에 저장하게 되어 JOIN할 필요를 없도록 함 

<br/><br/>

# 3. Scailing

> 확장 : 수직적, 수평적 확장이 존재<br/>
수직적 확장 : 단순히 데이터베이스의 성능을 향상시키는 것 <br/>
수평적 확장 : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미 → 하나의 DB에서 작동하지만 여러 호스트에서 작동함<br/>
> 

![image](https://user-images.githubusercontent.com/100047095/185764157-8c10b78f-e23b-4c95-897e-bb4faf40b567.png)

- 관계형 DB는 수직적 확장만을 지원함
- 수평적 확장은 NoSQL DB에서만 가능함
- SQL DB에서는 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방식인 샤딩을 이용하여 데이터를 저장해서 활용할 수 있기는 하지만 구현하기 대체로 어려움

<br/><br/>

# 4. 비교

![image](https://user-images.githubusercontent.com/100047095/185764149-51f78e94-9ea7-4196-a8e8-fe33711fcdc7.png)
<br/>
출처 : [https://overcome-the-limits.tistory.com/283](https://overcome-the-limits.tistory.com/283)
