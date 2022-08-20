# 1. JOIN

> 두 개 이상의 테이블을 결합하여 테이블을 검색하는 방법<br/>
검색하고 싶은 데이터가 한 개의 테이블이 아니라 여러 개의 테이블에 나누어져 있다면 각 테이블의 칼럼을 가져와 그 칼럼들을 접점으로 이용해 여러 테이블의 데이터를 검색하는 방식<br/>
접점 : 보통 Primary Key, Foreign Key로 두 테이블을 연결함<br/>
> 

<br/>

### 종류

- LEFT JOIN
- INNER JOIN
- FULL OUTER JOIN
- EXCLUSIVE JOIN
- CROSS JOIN
- SELF JOIN

보통 LEFT JOIN, INNER JOIN을 가장 많이 사용함 

<br/><br/>

# 2. 예시 테이블

**CAKE**

| ID | Name | DepNo |
| --- | --- | --- |
| 1 | 순우유 | 10 |
| 2 | 치즈 | 10 |
| 3 | 생크림 | 20 |
| 4 | 딸기 | 20 |
| 5 | 스초생 | 30 |
| 6 | 오레오 | 30 |
| 7 | 떡케이크 | NULL |

<br/>

**Dep**

| DepNo | DepName |
| --- | --- |
| 10 | 파리 |
| 20 | 뚜레 |
| 30 | 투썸 |
| 40 | 아티제 |

<br/><br/>

# 3. INNER JOIN

> INNER JOIN은 두 개의 테이블에서 공통된 요소들을 통해 결합하는 조인 방식임<br/>
가장 일반적인 JOIN으로 INNER JOIN 대신 JOIN을 입력해도 INNER JOIN이 사용됨
> 

![image](https://user-images.githubusercontent.com/100047095/185764013-dd52ac0b-e6c1-4bca-94aa-34bb389ce691.png)

출처 : [https://hongcoding.tistory.com/146](https://hongcoding.tistory.com/146)

<br/>

```sql
SELECT CAKE.Name, DEP.DepName
FROM CAKE JOIN DEP ON Cake.DepNo = Dep.DepNo
```

<br/>

**result**

| Name | DepName |
| --- | --- |
| 순우유 | 파리 |
| 치즈 | 파리 |
| 생크림 | 뚜레 |
| 딸기 | 뚜레 |
| 스초생 | 투썸 |
| 오레오 | 투썸 |

DepNo가 공통되지 않은 데이터인 null 값을 가진 떡케이크 행은 누락되어 있음 

INNER JOIN의 조건에 맞지 않기 때문에 맞는 데이터들만 출력됨

<br/><br/>

# 4. LEFT JOIN

> LEFT JOIN = LEFT OUTER JOIN<br/>
공통된 부분이 없는 데이터도 함께 보고 싶은 경우 사용하는 JOIN으로 LEFT OUTER JOIN은 공통된 값 + 왼쪽 테이블에만 있는 값이 출력됨
> 

![image](https://user-images.githubusercontent.com/100047095/185764087-d8813ba0-59a3-4a8c-bccb-b7473c784864.png)

```sql
SELECT Cake.Name, Dep.Name
FROM Cake LEFT JOIN Dep
ON Cake.DepNo = Dep.DepNo
```

<br/>

**result**

| Name | DepName |
| --- | --- |
| 순우유 | 파리 |
| 치즈 | 파리 |
| 생크림 | 뚜레 |
| 딸기 | 뚜레 |
| 스초생 | 투썸 |
| 오레오 | 투썸 |
| 떡케이크 | NULL |

<br/>

- 만약 여기서 공통된 부분마저도 제외하고 왼쪽 테이블에만 있는 항목들을 출력하고 싶은 경우 NULL을 이용하여 조건을 추가해주면 됨
    
    ```sql
    SELECT Cake.Name, Dep.Name
    From Cake LEFT JOIN Dep
    ON Cake.DepNo = Dep.DepNo
    WHERE Cake.DepNo IS NULL
    ```
    
<br/><br/>

# 5. RIGHT JOIN

> RIGHT JOIN = RIGHT OUTER JOIN<br/>
공통된 부분이 없는 데이터도 함께 보고 싶은 경우 사용하는 JOIN으로 RIGHT OUTER JOIN은 공통된 값 + 오른쪽 테이블에만 있는 값이 출력됨
> 

![image](https://user-images.githubusercontent.com/100047095/185764094-2fbbe467-f291-40c1-96e9-d66b8e0ea3e7.png)

```sql
SELECT Cake.Name, Dep.Name
FROM Cake RIGHT JOIN Dep
ON Cake.DepNo = Dep.DepNo
```

<br/>

**result**

| Name | DepName |
| --- | --- |
| 순우유 | 파리 |
| 치즈 | 파리 |
| 생크림 | 뚜레 |
| 딸기 | 뚜레 |
| 스초생 | 투썸 |
| 오레오 | 투썸 |
| NULL | 아티제 |

<br/><br/>

# 6. FULL OUTER JOIN

> 공통된 부분이 없는 데이터도 함께 보고 싶은 경우 사용하는 JOIN으로 FULL OUTER JOIN은 공통된 값 + 왼쪽 테이블만 가지고 있는 값 + 오른쪽 테이블만 가지고 있는 값이 출력됨<br/>
LEFT OUTER JOIN, RIGHT OUTER JOIN을 합친 것으로 볼 수 있음
> 

![image](https://user-images.githubusercontent.com/100047095/185764100-a2f5510d-1d47-449e-800a-5bf02218a231.png)

```sql
SELECT Cake.Name, Dep.Name
FROM Cake FULL OUTER JOIN Dep
ON Cake.DepNo = Dep.DepNo
```

<br/>

**result**

| Name | DepName |
| --- | --- |
| 순우유 | 파리 |
| 치즈 | 파리 |
| 생크림 | 뚜레 |
| 딸기 | 뚜레 |
| 스초생 | 투썸 |
| 오레오 | 투썸 |
| 떡케이크 | NULL |
| NULL | 아티제 |

<br/><br/>

# 7. CROSS JOIN

> CROSS JOIN은 두 테이블 간의 가능한 모든 경우의 수에 대한 결과를 보여줌<br/>
아래 예시에서는 Cake가 총 7행, Dep가 4행이었으므로 총 28행이 탄생하게 됨
> 

```sql
SELECT Cake.Name, Dep.DepName
FROM Cake CROSS JOIN Dep
```

<br/>

**result**

| Name | DepName |
| --- | --- |
| 순우유 | 파리 |
| 치즈 | 파리 |
| 생크림 | 파리 |
| 딸기 | 파리 |
| 스초생 | 파리 |
| 오레오 | 파리 |
| 떡케이크 | 파리 |
| 순우유 | 뚜레 |
| 치즈 | 뚜레 |
| … | … |
| 오레오 | 아티제 |
| 떡케이크 | 아티제 |


<br/><br/>

# 8. SELF JOIN

> SELF JOIN은 이름처럼 자기 혼자서 스스로 결합을 하는 방식<br/>
LEFT, RIGHT JOIN과는 다르게 스스로를 참조해서 결합을 함
> 

아래와 같은 테이블이 있을 때 각각의 Duo가 있는데 이때 Duo의 넘버가 아닌 이름을 알고 싶을 때 SELF JOIN을 사용 : 왜냐하면 Duo의 이름도 이 테이블 내에 존재하기 때문 

<br/>

**FOOD**

| ID | Name | Duo |
| --- | --- | --- |
| 1 | 아메리카노 | 4 |
| 2 | 콜라 | 5 |
| 3 | 맥주 | 6 |
| 4 | 치즈케이크 | 1 |
| 5 | 피자 | 2 |
| 6 | 나초 | 3 |

<br/>

```sql
SELECT A.ID, A.Name, B.Duo DuoName
FROM FOOD A JOIN FOOD B 
ON A.Duo = B.ID
```

<br/>

**result**

| ID | Name | DuoName |
| --- | --- | --- |
| 1 | 아메리카노 | 치즈케이크 |
| 2 | 콜라 | 피자 |
| 3 | 맥주 | 나초 |
| 4 | 치즈케이크 | 아메리카노 |
| 5 | 피자 | 콜라 |
| 6 | 나초 | 맥주 |
