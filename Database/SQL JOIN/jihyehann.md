# 💡 SQL - JOIN

## 1. 정의

JOIN(조인)이란, “두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법” 을 말한다.

<br/>

## 2. 종류

![image](https://user-images.githubusercontent.com/75151848/185726711-82da6232-57f3-414d-be3a-7325bf99ac00.png)

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

<br/>

> A는 기준 테이블, B는 조인 테이블이라고 하자.

### 1) INNER JOIN (내부 조인)

<img width="40%" src="https://user-images.githubusercontent.com/75151848/185726725-3d7d477e-77ac-453a-8375-1373af1b4dea.png" />

일반적으로 `JOIN` 을 말하면 `INNER JOIN` 을 의미한다.

두 테이블의 `교집합`, 즉 공통적인 부분을 조회한다.

#### MySQL

- 표준 SQL과는 달리 MySQL에서는 JOIN, INNER JOIN, CROSS JOIN이 모두 같은 의미로 사용된다.
- 조인 조건이 없다면 CROSS JOIN과 같은 결과를 반환한다.

```sql
SELECT A.NAME, B.AGE
FROM A
    [INNER] JOIN B ON 조인조건
[WHERE 검색조건];
```

#### Oracle

> 🔖 오라클 9i 까지는 **오라클 조인**만 사용할 수 있으며, 오라클 10g부터는 **안시 조인**을 추가로 사용할 수 있다.

```sql
-- 안시 조인
SELECT A.NAME, B.AGE
FROM A
    [INNER] JOIN B ON 조인조건
[WHERE 검색조건];

-- 오라클 조인
SELECT A.NAME, B.NAME
FROM A, B
WHERE 조인조건 [AND 검색조건];
```

<br/>

### 2) LEFT OUTER JOIN

<img width="40%" src="https://user-images.githubusercontent.com/75151848/185726740-8fa2ebd5-ccad-4a0b-ac0f-3f0ca33f7e32.png" />

두 테이블의 `교집합` + `기준 테이블의 값`을 조회한다.

즉, 공통 부분 외에 조인 테이블에 없는 값이더라도 기준 테이블의 값은 조회한다. (이때 조인 테이블의 컬럼은 모두 null 이다.)

#### MySQL

```sql
SELECT A.NAME, B.NAME
FROM A
    LEFT [OUTER] JOIN B ON 조인조건
[WHERE 검색조건];
```

#### Oracle

```sql
-- 안시 조인
SELECT A.NAME, B.NAME
FROM A
    LEFT OUTER JOIN B ON 조인조건
[WHERE 검색조건];

-- 오라클 조인
SELECT A.NAME, B.NAME
FROM A, B
WHERE A.컬럼이름 = B.컬럼이름(+) [AND 검색조건];
```


<br/>

### 3) RIGHT OUTER JOIN

<img width="40%" src="https://user-images.githubusercontent.com/75151848/185726794-76631386-a37b-4ac5-a504-0feb3ddc2048.png" />

두 테이블의 `교집합` + `조인 테이블의 값`을 조회한다.

이때는 조인 테이블에만 있는 데이터의 경우, 기준 테이블의 컬럼 값은 모두 null 이다.

#### MySql

```sql
SELECT A.NAME, B.NAME
FROM A
    RIGHT[OUTER] JOIN B ON 조인조건
[WHERE 검색조건];
```

#### Oracle

```sql
-- 안시 조인
SELECT A.NAME, B.NAME
FROM A
    RIGHT OUTER JOIN B ON 조인조건
[WHERE 검색조건];

-- 오라클 조인
SELECT A.NAME, B.NAME
FROM A, B
WHERE A.컬럼이름(+) = B.컬럼이름 [AND 검색조건];
```

<br/>

### 4) FULL OUTER JOIN

<img width="40%" src="https://user-images.githubusercontent.com/75151848/185726779-54ce9dbf-3c40-4a87-aadb-0be6c0749b08.png" />

두 테이블의 `합집합`을 조회한다.

#### MySQL

- MySQL은 FULL OUTER JOIN을 지원하지 않는다.
- 대신, LEFT OUTER JOIN과 RIGHT OUTER JOIN을 `UNION`해서 얻을 수 있다.

```sql
SELECT A.NAME, B.NAME
FROM A
    LEFT[OUTER] JOIN B ON 조인조건
[WHERE 검색조건]

UNION

SELECT A.NAME, B.NAME
FROM A
    RIGHT[OUTER] JOIN B ON 조인조건
[WHERE 검색조건];
```

> #### 💡 UNION vs UNION ALL
> - UNION [DISTINCT] : DISTINCT는 생략 가능하며, 중복 값을 제거한다.
> - UNION ALL : 중복 값을 제거하지 않아 UNION보다 속도가 빠르다.


#### Oracle

- FULL OUTER JOIN은 안시 조인에서만 사용 가능하다.

```sql
-- 안시 조인
SELECT A.NAME, B.NAME
FROM A
    FULL [OUTER] JOIN B ON 조인조건
[WHERE 검색조건];
```

<br/>

### 5) CROSS JOIN (상호 조인)

<img width="40%" src="https://user-images.githubusercontent.com/75151848/185731334-efd12473-1bd6-479a-80d7-6b0655e52b65.png" />

두 테이블의 모든 조합을 조회한다.

즉, 기준 테이블의 행 하나당 조인 테이블의 모든 행을 하나씩 조합한다.

만약 A 테이블의 row가 a개, B 테이블의 row가 b개라면, a x b 개의 데이터가 조회된다.

CROSS JOIN은 `카티션 곱(Catesian Product)`이라고도 부른다.

#### MySQL

```sql
SELECT A.NAME, B.NAME
FROM A
    CROSS JOIN B
[WHERE 검색조건];
```

#### Oracle

```sql
-- 안시 조인
SELECT A.NAME, B.NAME
FROM A
    CROSS JOIN B
[WHERE 검색조건];

-- 오라클 조인
SELECT A.NAME, B.NAME
FROM A, B
[WHERE 검색조건];
```


<br/>

### 6) SELF JOIN (자체 조인)

자신의 테이블과 조인한 결과를 조회한다.

하나의 테이블을 두 번 참조해야 하는 경우에 사용한다.

#### MySQL

```sql
SELECT A1.NAME, A2.NAME
FROM A A1
	JOIN A A2 ON 조인조건
[WHERE 검색조건];
```

#### Oracle

```sql
-- 안시 조인
SELECT A1.NAME, A2.NAME
FROM A A1 
	JOIN A A2 ON 조인조건
[WHERE 검색조건];

-- 오라클 조인
SELECT A1.NAME, A2.NAME
FROM A A1, A A2
WHERE 조인조건 [AND 검색조건];
```


<br/><br/>

## 🔖  참고
- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Database/[Database SQL] JOIN.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDatabase%20SQL%5D%20JOIN.md)
- [https://pearlluck.tistory.com/46](https://pearlluck.tistory.com/46)
- [http://www.tcpschool.com/mysql/mysql_multipleTable_join](http://www.tcpschool.com/mysql/mysql_multipleTable_join)
- [https://jaehoney.tistory.com/55](https://jaehoney.tistory.com/55)
- [https://gent.tistory.com/469](https://gent.tistory.com/469)
