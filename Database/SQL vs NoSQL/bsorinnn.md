# SQL vs NoSQL

## A. SQL(관계형 DB)

SQL 이용 시 RDBMS에서 데이터를 저장, 수정, 삭제 및 검색할 수 있다.

<br>

RDBMS의 특징 두 가지

- 데이터는 **정해진 데이터 스키마에 따라 테이블에 저장**
- 데이터는 **관계를 통해 여러 테이블에 분산**

<br>

```
📌 용어 정리:

- 스키마
데이터베이스를 구성하는 개체(Entity), 속성(Attribute), 관계(Relationship) 및 제약조건(Constraint) 등에 대해 전반적으로 정의한 메타데이터의 집합

- 관계(Relationship)
개체와 개체가 맺고 있는 의미 있는 연관성
개체 집합들 사이의 대응 관계, 즉 매핑(mapping)을 의미

- 릴레이션(relation)
하나의 개체에 관한 데이터를 2차원 테이블의 구조로 저장한 것
파일 관리 시스템 관점에서 파일(file)에 대응
```

데이터는 테이블에 레코드로 저장되는데, 각 테이블마다 명확하게 정의된 구조가 있다. 해당 구조는 필드의 이름과 데이터 유형으로 정의된다. <Br>
=> 따라서 **스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없다**

<br>

또한 관계를 이용하기 때문에 하나의 테이블에서 중복 없이 하나의 데이터만을 관리한다.
다른 테이블에서 부정확한 데이터를 다룰 위험이 없어진다는 장점이 있다.

<br>

**SQL 장점**

- 명확하게 정의된 스키마, 데이터 무결성 보장
- 관계는 각 데이터를 중복없이 한번만 저장

**SQL 단점**

- 덜 유연함. 데이터 스키마를 사전에 계획하고 알려야 함. (나중에 수정하기 힘듬)
- 관계를 맺고 있어서 조인문이 많은 복잡한 쿼리가 만들어질 수 있음
- 대체로 수직적 확장만 가능함

<br>

+) 수직적 확장이란?

데이터베이스 서버의 확장성은 '수직적' 확장과 '수평적' 확장으로 나누어진다.

- 수직적 확장 : 단순히 데이터베이스 서버의 성능을 향상시키는 것 (ex. CPU 업그레이드)
- 수평적 확장 : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미 (하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동)
  > 데이터 저장 방식으로 인해 SQL 데이터베이스는 일반적으로 수직적 확장만 지원함

<br>

## B. NoSQL(비관계형 DB)

SQL의 반대 개념.

**스키마도 없고 관계도 없다**

SQL은 정해진 스키마를 따르지 않는다면 데이터 추가가 불가능한 반면, NoSQL에서는 다른 구조의 데이터를 같은 컬렉션에 추가가 가능하다.

NoSQL는 레코드를 문서(document)라고 한다.

문서는 Json과 비슷한 형태로 가지고 있다. 관계형 데이터베이스처럼 여러 테이블에 나누어담지 않고, 관련 데이터를 동일한 '컬렉션'에 넣는다.

<br>

**NoSQL 장점**

- 스키마가 없어서 유연함. 언제든지 저장된 데이터를 조정하고 새로운 필드 추가 가능
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장됨. 데이터 읽어오는 속도 빨라짐
- 수직 및 수평 확장이 가능해서 애플리케이션이 발생시키는 모든 읽기/쓰기 요청 처리 가능

**NoSQL 단점**

- 유연성으로 인해 데이터 구조 결정을 미루게 될 수 있음
- 데이터 중복을 계속 업데이트 해야 함
- 데이터가 여러 컬렉션에 중복되어 있기 때문에 수정 시 모든 컬렉션에서 수행해야 함 (SQL에서는 중복 데이터가 없으므로 한번만 수행이 가능)

<br>

### NoSQL 데이터베이스의 종류

<br>

- Documnet-based databases
- Key-value stores
- Column-oriented databases
- Graph-based databases

<br>

#### Document-based database(문서 데이터베이스)

<br>

```JSON
[
    {
        "year" : 2013,
        "title" : "Turn It Down, Or Else!",
        "info" : {
            "directors" : [ "Alice Smith", "Bob Jones"],
            "release_date" : "2013-01-18T00:00:00Z",
            "rating" : 6.2,
            "genres" : ["Comedy", "Drama"],
            "image_url" : "http://ia.media-imdb.com/images/N/O9ERWAU7FS797AJ7LU8HN09AMUP908RLlo5JF90EWR7LJKQ7@@._V1_SX400_.jpg",
            "plot" : "A rock band plays their music at high volumes, annoying the neighbors.",
            "actors" : ["David Matthewman", "Jonathan G. Neff"]
        }
    },
    {
        "year": 2015,
        "title": "The Big New Movie",
        "info": {
            "plot": "Nothing happens at all.",
            "rating": 0
        }
    }
]
```

<br>

데이터를 테이블의 행과 열에 저장하는 대신, **JSON 유사 형식의 문서로 데이터를 저장 및 쿼리**하도록 설계된 비관계형 데이터베이스.

- 애플리케이션 코드에서 사용하는 것과 동일한 문서 모델 형식을 사용하여 데이터베이스에서 보다 손쉽게 데이터를 저장하고 쿼리할 수 있다.

- 유연하고 구조화되지 않았기 때문에 애플리케이션 요구를 발전시키는 데 유리하다

- 오픈 포맷: 문서 생성 시 JSON, XML, CML, YAML 등으로 생성할 수 있다.

- 생성과 유지가 쉽다

- ex) MongoDB, CouchDB

<br>

#### Key-value stores(키-값 데이터베이스)

<img src="https://d1.awsstatic.com/product-marketing/DynamoDB/PartitionKey.8dd0530a7f6d66d101f31de30db515564f4cf28a.png" height=180>

간단한 **키-값 메소드**를 사용하여 데이터를 저장하는 비관계형 데이터베이스

- 키를 고유한 식별자로 사용하는 키-값 쌍의 집합으로 데이터를 저장
- 키-값은 문자, 숫자, 객체로 묶인 키-값도 설정 가능하다.
- 파티셔닝이 가능하고 다른 유형의 데이터베이스로는 불가능한 범위까지 수평 확장을 가능하게 한다
- 사용 사례: 세션 스토어, 장바구니
- ex) Redis, DynamoDB

<br>

#### Column-oriented databases

<br>

<img src="https://www.timestored.com/time-series-data/images/column-vs-row-oriented-database.png" heigh=150>

<br>

데이터를 행 대신 **열(column)에 저장**하는 비관계형 데이터베이스.

- 기존 열이 영향을 받지 않으므로 다른 열을 쉽게 추가할 수 있다.
- 각 열을 별도로 저장하면 소수의 열만 포함된 경우 더 빨리 검색할 수 있다.
- 주요 특징: 확장성, 압축
- ex) Cassandra, HBase

<br>

#### Graph-based databases

<br>

<img src="https://d1.awsstatic.com/diagrams/foaf-graph.e5e42865e0ee97a2972f9014d28f525ef68a981b.png" heigh=150>

<br>

- 관계를 저장하고 탐색하도록 구축
- 노드를 사용하여 데이터 엔터티를 저장하고 엣지로는 엔터티 간의 관계를 저장
- 노드 간 관계는 쿼리 시간에는 포함되지 않지만 데이터베이스에서 유지되기 때문에 조인 또는 관계를 트래버스 하는 속도가 빠름
- 데이터 간 관계가 있고 관계 신속히 처리해야 하는 사례에서 사용
  - 소셜 네트워크, 추천 엔진, 이상 탐지
- ex) Neo4j, Amazon Neptune

<br>

## C. SQL vs NoSQL

<br>

| DBMS                | SQL 데이터베이스          | NoSQL 데이터베이스            |
| ------------------- | ------------------------- | ----------------------------- |
| 종류(Type)          | 관계형 데이터베이스       | 비관계형 데이터베이스         |
| 구조(Structure)     | 테이블 구조               | 문서 구조(document)           |
| 스키마(Schema)      | 정해진 스키마 따라야 한다 | 스키마가 없어 유연하다        |
| 확장성(Scalability) | 수직적 확장               | 수직/수평적 확장              |
| 쿼리(Query)         | SQL 사용                  | 데이터베이스 유형에 따라 다름 |

<br>

### SQL 데이터베이스 사용이 더 좋을 때

- 관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션의 경우

  > NoSQL에서는 여러 컬렉션을 모두 수정해야 하기 때문에 비효율적

- 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우

<br>

### NoSQL 데이터베이스 사용이 더 좋을 때

- 정확한 데이터 구조를 알 수 없거나 변경/확장 될 수 있는 경우
- 읽기를 자주 하지만, 데이터 변경은 자주 없는 경우
  데이터베이스를 수평으로 확장해야 하는 경우 (막대한 양의 데이터를 다뤄야 하는 경우)

<br>

## C. 참고자료

🔗 https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html

🔗 https://redis.com/nosql/what-is-nosql/

🔗 https://aws.amazon.com/ko/nosql/

🔗 https://www.mongodb.com/nosql-explained/nosql-vs-sql
