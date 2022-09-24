# 인덱스 (INDEX)

## A. 인덱스

**인덱스의 목적**

> 💡 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 **검색 속도를 향상시키기 위한** 자료구조

- INDEX는 색인

_책의 목차같은 개념이라고 생각하면 쉽다_

- 해당 Table의 Column을 색인화(따로 파일로 저장)하여 해당 Table의 레코드를 full scan하는 것이 아니라, 색인화되어 있는 INDEX 파일을 검색하여 검색 속도를 빠르게 한다.

- INDEX 구조는 Tree 구조로 색인화한다.

- RDBMS에서 사용하는 INDEX는 B+Tree를 사용한다.

<br/>

## B. 인덱스의 동작 원리

<br/>

INDEX를 해당 컬럼에 주게 되면 초기 Table 생성 시 **FRM, MYD, MYI** 3 개의 파일이 생성된다.

- **FRM**: 테이블 구조가 저장되어 있는 파일
- **MYD**: 실제 데이터가 있는 파일
- **MYI**: INDEX 정보가 들어있는 파일 (INDEX 미사용시 비워져 있다)

INDEX를 해당 컬럼에 주게 되면 해당 컬럼을 따로 인덱싱하여 MYI 파일에 입력한다.

이후 사용자가 SELECT 쿼리로 INDEX를 사용하는 쿼리를 사용 시 해당 Table을 검색하는 것이 아니라 **MYI 파일의 내용을 검색**한다.

만약, INDEX를 사용하지 않는 SELECT 쿼리라면 해당 Table을 Full scan 하여 모두 검색한다.

<p align="center" style="color:gray">
<img src="https://github.com/WeareSoft/tech-interview/raw/master/contents/images/db-index.png" height=180>
</p>

SCOUNTER TABLE 생성 시 AIRPORT 칼럼에 대한 인덱스 테이블이 생성된다.

SCOUNTER TABLE에 AIRPORT 칼럼에 대한 WHERE 문이 포함된 쿼리가 나갈 때 AIRPORT 인덱스 테이블에 저장된 Key-value 값을 참조하여 SCOUNTER 테이블에서 결괏값을 반환한다.

**동작 방법**

- Index Table에서 where에 포함된 값을 찾는다.
- 해당 값의 table_id[PK]를 가져온다
- 가져온 table_id[PK] 값으로 원본 테이블에서 값을 조회해온다.

<br/>

## C. 추가 내용

### 📌 인덱스의 장단점

<br/>

**장점**

- 테이블을 검색하는 속도와 성능이 향상 → 시스템의 전반적인 부하 줄일 수 있다.

👉  핵심: 인덱스에 의해 데이터들이 정렬된 형태를 갖는다는 것.

**단점**

- Index 생성 시, .mdb 파일 크기가 증가한다.

  _.mdb: Microsoft Database를 나타내는 Microsoft Access Database_

- **사용자가 한 페이지를 동시에 수정할 수 있는 병행성**이 줄어든다.
- 인덱스된 Field에서 데이터를 업데이트하거나, **Record를 추가 또는 삭제 시 성능이 떨어진다**.
- 데이터 변경 작업이 자주 일어나는 경우, **Index를 재작성**해야 하므로 성능에 영향을 미친다.
- 인덱스가 데이터베이스 공간을 차지해 추가적인 공간이 필요해진다.(DB의 10% 내외의 공간이 추가로 필요하다.)

<br/>

### INDEX를 사용하면 좋은 경우

INDEX를 효율적으로 사용하기 위해서는 데이터의 Range가 넓고, 중복이 적고, 조회가 많거나 정렬된 상태가 유용한 컬럼에 사용하는 것이 좋다. 따라서 다음과 같은 경우에 INDEX를 사용하면 효율적이다.

(1) 규모가 큰 테이블

(2) DML이 자주 발생하지 않는 컬럼

(3) WHERE나 ORDER BY, JOIN 등이 자주 사용되는 컬럼

(4) 데이터의 중복도가 낮은 컬럼

<br/>

### INDEX 사용을 피해야 하는 경우

(1) 데이터 중복도가 높은 컬럼(카디널리티가 낮은 컬럼)
→ 인덱스로 만들어도 무용지물(e.g.성별)

(2) DML이 자주 일어나는 Column
→ DML에 취약

<br/>

### +) DML이란?

> 📌 DML(Data Manipulation Langauge): 데이터 조작어

1. `INSERT`

: 테이블에는 입력 순서대로 저장되지만, 인덱스 테이블에는 정렬하여 저장하기 때문에 성능 저하 발생

1. **index split**: 인덱스의 Block들이 하나에서 두개로 나누어지는 현상.
2. 인덱스는 데이터가 순서대로 정렬되어야 한다. 기존 블록에 여유 공간이 없는 상황에서 그 블록에 새로운 데이터가 입력되어야 할 경우, 오라클이 기존 블록의 내용 중 일부를 새 블록에다가 기록한 후, 기존 블록에 빈 공간을 만들어서 새로운 데이터를 추가하게 된다.
3. 성능면에서 매우 불리하다.
   1. Index split은 새로운 블록을 할당받고 Key를 옮기는 복잡한 작업을 수행한다. 모든 수행 과정이 Redo에 기록되고 많은 양의 Redo를 유발한다.
   2. Index split이 이루어지는 동안 해당 블록에 대해 키 값이 변경되면 안되므로 DML이 블로킹된다. (대기 이벤트 발생)

<br/>

2. `DELETE`

: 테이블에서만 삭제되고 인덱스 테이블에는 남아있어 쿼리 수행 속도 저하

<Table과 Index 상황 비교>

1. 테이블에서 데이터가 Delete될 경우, 지워지고 다른 데이터가 그 공간을 사용할 수 있다.
2. i**ndex에서 데이터가 delete될 경우, 데이터가 지워지지 않고 사용 안됨 표시만 해둔다.**
3. 즉, 테이블에 데이터가 1만건 있는 경우, 인덱스에는 2만건이 있을 수 있다는 뜻이다.
4. 인덱스를 사용해도 수행 속도를 기대하기 힘들다.

<br/>

3. `UPDATE`

: 인덱스에는 UPDATE가 없기 때문에 DELETE, INSERT 두 작업 수행하여 부하 발생

1. **인덱스에는 Update 개념이 없다.**
2. 따라서 테이블에 update가 발생할 경우, 인덱스에서는 delete가 먼저 발생한 후 새로운 작업의 insert 작업이 발생한다.
3. **delete와 insert 두 개의 작업이 인덱스에서 동시에 일어나 다른 DML보다 더 큰 부하를 주게 된다.**

<br/>

## D. 참고한 페이지

<br/>

🔗 [[DB] Index.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Index.md)

🔗 [Database](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#index)

🔗 [db.md#index란](https://github.com/WeareSoft/tech-interview/blob/master/contents/db.md#index%EB%9E%80)
