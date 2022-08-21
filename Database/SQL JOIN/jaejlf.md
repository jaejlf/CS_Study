# 📍 Join

- 하나 이상의 테이블을 연결하여 데이터를 검색하는 방법
- 둘 이상의 테이블을 연결하려면, 적어도 하나의 컬럼을 공유하고 있어야 한다.

<br>

## 내부 조인 (INNER JOIN)

- `교집합`, 공통적인 부분만 추출하는 조인
- `INNER JOIN` 절 사용할 경우 조건절에 `WHERE` 대신 `ON`
- INNER 키워드 생략 가능

<br>

![image](https://user-images.githubusercontent.com/78673570/185739695-338de274-b6f8-4d63-9999-78c418756c0f.png)

```sql
SELECT Table_A.id, Table_A.name, Table_A.day, Table_B.email
FROM Table_A, Table_B
WHERE Table_A.id = Table_B.id;
```
```sql
SELECT Table_A.id, Table_A.name, Table_A.day, Table_B.email
FROM Table_A INNER JOIN Table_B
ON Table_A.id = Table_B.id;
```

<br>

💡 USING 키워드 : 조인하고자 하는 두 테이블의 컬럼명이 같을 경우 간단하게 적을 수 있도록 하는 역할

```sql
SELECT Table_A.id, Table_A.name, Table_A.day, Table_B.email
FROM Table_A INNER JOIN Table_B
USING(id);
```

<br>

### 등가 조인 (Equi Join)

- 조인 조건에서 `Equality Condition(=)`을 사용하여 값들이 `정확하게 일치하는 경우`에 사용하는 조인
- 대부분 기본 키와 외래 키의 관계를 이용하여 조인
- `테이블 별칭(= AS, Alias)`를 가독성 좋게 명시해주는 것이 좋다.

<br>

```sql
SELECT A.id, A.a_name, B.b_name
FROM TableA A, TableB B
WHERE A.id = B.id;
```
```sql
SELECT A.id, A.a_name, B.b_name
FROM TableA A, TableB B
WHERE A.id = B.id AND A.id >= 2;
```

<br>

💡 테이블 별칭(= AS, Alias)

- 테이블 별칭을 이용해 긴 테이블 이름을 간단하게 사용
- 테이블 별칭은 현재 SELECT SQL문에서만 유효
- FROM절에 테이블 별칭이 사용되면 SELECT문 전체에서 사용 가능

<br>

### 자연 조인 (Natural Join)

- 두 테이블 간에 `공통적으로 나타나는 필드`를 조인
- 같은 이름을 가진 컬럼은 한 번만 추출

<br>

![image](https://user-images.githubusercontent.com/78673570/185740020-9dda298b-4b52-41d4-88a8-0ecdc358c0d4.png)

```sql
SELECT *
FROM Table_A NATURAL JOIN Table_B
```

<br>

---

<br>

## 외부 조인 (Outer Join)

- `정상적으로 조인 조건을 만족하지 못하는 행들까지` 추출하고 싶을 때 사용하는 조인 <br> (Inner Join, Equi Join의 경우 조인하는 테이블 간 공통된 값이 없다면 행을 반환하지 않는다.)
- 조인시킬 값이 없는 쪽에 `(+)`
- `(+)` 연산자는 표현식의 한 쪽에만 사용 가능
- Outer join은 `IN` 연산자를 사용할 수 없고, `OR` 연산자에 의해 다른 조건에 연결될 수 없다.

<br>

### Right Outer Join

- `오른쪽 → 왼쪽 순서`
- `오른쪽`에 있는 테이블의 데이터를 가져온 후, `왼쪽` 테이블의 데이터를 매칭하고 매칭되는 데이터가 없는 경우 `NULL`로 표시

<br>

![image](https://user-images.githubusercontent.com/78673570/185740662-a2e8305c-0778-494b-aaa5-9dd6c86a27e2.png)

```sql
SELECT *
FROM Table_A, Table_B
WHERE Table_A.id(+) = Table_B.id;
```
```sql
SELECT *
FROM Table_A RIGHT OUTER JOIN Table_B
ON Table_A.id = Table_B.id;
```

<br>

### Left Outer Join

- `왼쪽 → 오른쪽 순서`
- `왼쪽`에 있는 테이블의 데이터를 가져온 후, `오른쪽` 테이블의 데이터를 매칭하고 매칭되는 데이터가 없는 경우 `NULL`로 표시

<br>

![image](https://user-images.githubusercontent.com/78673570/185741146-016a1e4a-44b6-4d28-9ffe-a12137fa23f9.png)

```sql
SELECT *
FROM Table_A, Table_B
WHERE Table_A.id = Table_B.id(+);
```
```sql
SELECT *
FROM Table_A LEFT OUTER JOIN Table_B
ON Table_A.id = Table_B.id;
```

<br>

### Full Outer Join

- MySQL에는 FULL Outer Join X
- (+) 연산자를 양쪽에 쓰는 쿼리문은 오류

<br>

![image](https://user-images.githubusercontent.com/78673570/185741414-50e28f88-43d4-4921-b2f5-b94ba55faa66.png)

```sql
SELECT *
FROM Table_A FULL OUTER JOIN Table_B
ON Table_A.id = Table_B.id;
```

<br>

---

<br>

## 크로스 조인 (Cross Join)

= 카티션 곱 (Cartesian Product)

- 발생 가능한 `모든 경우의 수`의 행이 출력되는 것
    - N개 행을 가진 테이블과 M개 행을 가진 테이블의 카티션 곱은 `N * M`
- 검색하고자 했던 데이터 뿐 아니라 조인에 사용되는 테이블의 모든 데이터가 반환
- 카티션 곱이 발생하는 경우
    1. 조인 조건을 정의하지 않았을 경우
    2. 조인 조건이 잘못된 경우
    3. 첫 번째 테이블의 모든 행들이 두 번째 테이블의 모든 행과 조인되는 경우

<br>

![image](https://user-images.githubusercontent.com/78673570/185740309-249b54ce-e719-45c6-9e0e-493bda87abbd.png)

```sql
-- 조인 조건을 정의하지 않은 경우
SELECT *
FROM Table_A, Table_B;
```
    
<br>

## 비등가 조인 (Non-Equi Join)

- 두 개의 테이블 간에 컬럼 값들이 `서로 정확하게 일치하지 않는 경우`에 사용되는 조인
- Equality Condition(=) 이외의 연산자 사용 : `BETWEEN - AND`, `IS NULL`, `IS NOT NULL`, `IN`, `NOT IN`

```sql
SELECT *
FROM TableA A, TableB B
WHERE B.id BETWEEN 1 AND 3;
```

<br>

## 자체 조인 (Self Join)

- 동일 테이블 사이의 조인
- FROM 절에 동일 테이블이 두 번 이상 나타난다. ⇒ 반드시 `테이블 별칭(= AS, Alias)`을 사용해야 한다.

```sql
SELECT e1.empno, e1.ename, e2.empno AS MGRNO, e2.ename AS MGRNAME
FROM EMP e1, EMP e2
WHERE e1.mgr = e2.empno;
```
