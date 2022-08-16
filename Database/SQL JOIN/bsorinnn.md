# SQL JOIN

#### 조인이란?

> 두 개 이상의 테이블이나 데이터베이스를 연결하는 것

테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용합니다.

<br>

#### JOIN의 종류

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

<br>

- **(INNER) JOIN**

<img src="https://www.w3schools.com/sql/img_innerjoin.gif">

<br>

교집합으로, 기존 table과 Join table의 중복된 값을 나타냅니다.<br>
결과값은 A 테이블과 B 테이블이 **모두 가지고 있는 데이터**만 검색됩니다.

<br>

```SQL
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

🗒 INNER JOIN은 두 테이블이 모두 가지고 있는 데이터만 검색되므로, 한 테이블만 가지고 있는 데이터는 표시되지 않습니다.

<br>

- **LEFT (OUTER) JOIN**

<img src="https://www.w3schools.com/sql/img_leftjoin.gif">

<br>

기준 테이블 값과 조인 테이블과 중복된 값을 보여줍니다.

**왼쪽 테이블 기준**으로 JOIN을 한다고 생각하면 편합니다.<br>
결과값은 `table1` 테이블의 모든 값과 `table2` 테이블의 중복되는 값이 검색됩니다.

<br>

```SQL
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

🗒 LEFT (OUTER) JOIN은 오른쪽 테이블(table2)와 중복되는 값이 없더라도, 왼쪽 테이블(table1)의 모든 레코드를 리턴합니다.

<br>

- **RIGHT (OUTER) JOIN**

<img src="https://www.w3schools.com/sql/img_rightjoin.gif">

<br>

`LEFT OUTER JOIN`과는 반대로 **오른쪽 테이블 기준**으로 JOIN합니다.

<br>

```SQL
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

🗒 RIGHT (OUTER) JOIN은 왼쪽 테이블(table1)와 중복되는 값이 없더라도, 오른쪽 테이블(table2)의 모든 레코드를 리턴합니다.

<br>

- **FULL (OUTER) JOIN**

<img src="https://www.w3schools.com/sql/img_fulljoin.gif">

<br>

**합집합**으로, A와 B 테이블의 모든 데이터가 검색됩니다.<br>

A 테이블이 가지고 있는 데이터, B 테이블이 가지고 있는 **데이터가 모두 검색되므로,** 사실상 기준 테이블의 의미가 없습니다.

<br>

```SQL
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;
```

🗒 FULL OUTER JOIN은 두 테이블의 모든 데이터를 표시하므로, table1에는 일치하지만 table2에는 일치하지 않는 행이나 반대로 table2에는 일치하지만 table1에는 일치하지 않는 행도 표시합니다.

<br>

- **LEFT (OUTER) JOIN**

<img src="https://www.w3schools.com/sql/img_leftjoin.gif">

<br>

기준 테이블 값과 조인 테이블과 중복된 값을 보여줍니다.

**왼쪽 테이블 기준**으로 JOIN을 한다고 생각하면 편합니다.<br>
결과값은 `table1` 테이블의 모든 값과 `table2` 테이블의 중복되는 값이 검색됩니다.

<br>

```SQL
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

🗒 LEFT (OUTER) JOIN은 오른쪽 테이블(table2)와 중복되는 값이 없더라도, 왼쪽 테이블(table1)의 모든 레코드를 리턴합니다.

<br>

- **RIGHT (OUTER) JOIN**

<img src="https://www.w3schools.com/sql/img_rightjoin.gif">

<br>

`LEFT OUTER JOIN`과는 반대로 **오른쪽 테이블 기준**으로 JOIN합니다.

<br>

```SQL
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

🗒 RIGHT (OUTER) JOIN은 왼쪽 테이블(table1)와 중복되는 값이 없더라도, 오른쪽 테이블(table2)의 모든 레코드를 리턴합니다.

<br>

- **CROSS JOIN**

<img src="https://camo.githubusercontent.com/c8170fd119eac82de056d7b1659824b1d398627fa09cccb70553becd4906d146/68747470733a2f2f696d67312e6461756d63646e2e6e65742f7468756d622f523132383078302f3f73636f64653d6d746973746f72793226666e616d653d687474702533412532462532466366696c6531302e75662e746973746f72792e636f6d253246696d61676525324639393346344534343541384132443238314143363642">

<br>

모든 경우의 수를 전부 표현해주는 방식입니다.<br>

A가 3개, B가 4개면 총 3\*4 = 12개의 데이터가 검색됩니다.

<br>

```SQL
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```

<br>

- **SELF JOIN**

<img src="https://camo.githubusercontent.com/3600303a038c6cc6f6189738e96de0f791673b542f84c1895afa9b32a4fb6208/68747470733a2f2f696d67312e6461756d63646e2e6e65742f7468756d622f523132383078302f3f73636f64653d6d746973746f72793226666e616d653d687474702533412532462532466366696c6532352e75662e746973746f72792e636f6d253246696d61676525324639393334314433333541384133363344303631344538">

<br>

자기 자신과 조인하는 것을 말합니다.<br>
하나의 테이블을 여러 번 복사해서 조인한다고 생각해도 좋습니다.

자신이 가지고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용합니다.

<br>

```SQL
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```

<br>

### 번외

<br>

#### JOIN VS Subquery

- JOIN: 두 개 이상의 테이블의 레코드를 결합하는 쿼리
- Subquery(= Inner query, Nested query): SQL 쿼리 내의 쿼리이며 WHERE 문에 포함되어 있다.

JOIN

```SQL
SELECT
 p.name,
 p.cost
FROM product AS p
JOIN sale AS s
  ON p.id = s.product_id
WHERE s.price = 2000;
```

Subquery

```SQL
SELECT name, cost
FROM product
WHERE id =
( SELECT product_id
   FROM sale
   WHERE price = 2000
        AND product_id = product.id );
```

JOIN의 장점

- JOIN을 사용하는 쿼리의 검색 시간은 거의 항상 서브쿼리보다 빠르다
- JOIN을 사용하면 서브쿼리처럼 여러 개의 쿼리를 사용할 필요 없이 JOIN 쿼리만 사용하면 되므로 데이터베이스의 계산 부담을 덜어준다.

<br>

JOIN의 단점

- JOIN을 사용할 경우 서브 쿼리만큼 읽기 쉽진 않다
- 쿼리에 JOIN이 많을 수록 데이터베이스 서버가 더 많은 작업을 수행해야 하므로 데이터 검색에 더 많은 시간이 소요된다
- JOIN의 종류가 다양하므로 원하는 결과를 얻기 위해서는 어떤 JOIN을 사용해야 할지 헷갈릴 수 있다
- JOIN을 올바르지 않게 수행할 경우 심각한 성능 저하와 부정확한 쿼리 결과가 발생할 수 있다.

<br>

서브쿼리의 장점

- 복잡한 쿼리를 각각의 독립된 부분으로 나누므로 논리적으로 파악하기 쉽다
- 이해하기 쉽고 코드 유지 보수가 쉽다
- 서브쿼리를 사용할 시 외부 쿼리의 쿼리 결과를 사용할 수 있다
- 경우에 따라 서브쿼리가 복잡한 JOIN 이나 UNION을 대체할 수 있다

<br>

서브쿼리의 단점

- 대부분의 경우 서브쿼리를 사용하는 SQL문을 JOIN으로 다시 작성하면 더 효율적으로 실행할 수 있다

<br>

#### JOIN 사용 시 주의해야 할 점

결과 set의 행 수를 증가시키는 방식으로 두 테이블을 JOIN할 경우 쿼리가 느려질 수 있으므로 이를 주의해야 한다.

=> 테이블 크기를 줄인 뒤 JOIN을 사용하는 걸 추천한다

## 참고자료

🔗 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDatabase%20SQL%5D%20JOIN.md

🔗 https://www.w3schools.com/sql/sql_join.asp

🔗 https://www.geeksforgeeks.org/sql-join-vs-subquery/

🔗 https://mode.com/sql-tutorial/sql-performance-tuning/
