# 1. SQL Injection

악의적인 사용자가 보안상의 취약점을 이용하여 임의의 SQL 문을 주입하고 실행하게 하여 데이터베이스가 비정상적으로 동작하게 조작하는 행위

<br/>

**종류**

- Error Based SQL Injection
- Union Based SQL Injection
- Blind SQL Injection
    - Boolean Based SQL
    - Time Based SQL
- Stored Procedure SQL Injection
- Mass SQL Injection

<br/><br/>

# 2. Error Based SQL Injection

> 논리적 에러를 이용한 SQL Injection<br/>
가장 많이 쓰이고 대중적인 공격 기법
> 

<br/>

**ex)**

1. 공격 대상 : `SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'`
2. 공격 예시 : `SELECT * FROM Users WHERE id = '' OR 1=1 -- ' AND password = 'INPUT2'`

→ 싱글 쿼터를 닫아주기 위한 싱글쿼터와 OR 1=1 구문을 이용해 where 뒤의 절을 모두 참으로 만들고 --를 넣어줌으로써 뒤의 구문을 주석 처리함

→ 결론 : Users table에 있는 모든 정보를 조회하게 되어 가장 먼저 만들어진 계정 (보통 관리자 계정) 으로 로그인할 수 있게 되어 관리자 계정이 탈취됨

<br/><br/>

# 3. UNION Based SQL Injection

> Union : 두 개의 쿼리문에 대한 결과를 통합해서 하나의 테이블로 보여주게 하는 키워드<br/>
정상적인 쿼리문에 Union 키워드를 사용하여 인젝션에 성공하면 원하는 쿼리를 실행할 수 있음
> 

<br/>

**Union Injection에 성공하기 위한 조건**

- Union하는 두 테이블의 칼럼 수가 같아야 함
- Union하는 두 테이블의 데이터 형이 같아야 함

<br/>

**ex)**

1. 공격 대상 : `SELECT * FROM Board WHERE title LIKE '%INPUT%' OR contents '%INPUT%'`
2. 공격 예시 : `SELECT * FROM Board WHERE title LIKE '% ' UNION SELECT null,id,passwd FROM Users -- INPUT%' OR contents '%INPUT%'`

→ Board라는 테이블의 게시글을 검색하는 쿼리문임. 여기서 입력값을 title과 contents 칼럼의 데이터와 비교한 뒤 비슷한 글자가 있는 게시글을 출력함.

→ 그러나 여기에 입력값으로 UNION 키워드와 함께 SELECT 문으로 유저 테이블을 조회하는 구문을 넣게 되면 두 쿼리문이 합쳐져서 하나의 테이블로 보이게 됨

→ 결론 : 사용자의 id와 pwd를 요청하는 쿼리문이 주입되어 사용자의 개인정보가 게시글과 함께 화면에 보여지게 됨

<br/><br/>

# 4. Blind SQL Injection - Boolean Based SQL

> limit, SUBSTR, ASCII… 등의 SQL 문을 사용<br/>
특정한 값이나 데이터를 전달받는 것이 아닌 쿼리를 통해 나온 t/f 값으로 정보를 취득
> 
- 에러가 발생하지 않는 사이트에서는 논리적 에러를 이용하거나 UNION을 이용할 수 없기 때문에 Blind를 통해 정상적인 쿼리가 수행되는지 혹은 쿼리가 되지 않아 쿼리 결과가 없는지 판단
- 서버가 응답하는 성공과 실패 여부를 이용하여 DB의 테이블 정보 등을 추출해 낼 수 있음

<br/>

**ex)**

1. 공격 대상 : `SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'`
2. 공격 예시 : `SELECT * FROM Users WHERE id = 'abc123' and ASCII(SUBSTR((SELECT name FROM information_schema.tables WHERE table_type='base table' limit 0,1),1,1)) > 100 (로그인이 될 때까지 시도) -- INPUT1' AND password = 'INPUT2'`

→ 이 쿼리문은 DB의 테이블 명을 알아내는 쿼리문임

→ 임의로 가입한 abc123이라는 아이디와 함께 뒤의 문구를 주입하는 것인데 이 구문은 테이블 명을 조회하는 구문으로 limit 키워드를 통해 하나의 테이블만 조회하고 SUBSTR 함수로 첫 글자만, ASCII를 통해 아스키 값으로 변환함 그리고 그 값을 100이라는 숫자와 비교함

→ 결론 : 자동화된 스크립트를 이용해 단기간 내에 테이블 명을 알아낼 수 있음 

<br/><br/>

# 5. Blind SQL Injection - Time Based SQL

> SLEEP, BENCHMARK… 등의 SQL 문을 사용하여 쿼리 결과를 특정 시간만큼 지연시킴<br/>
에러가 발생되지 않는 조건에서 사용하며 참, 거짓이라는 결과값이 나오지 않으므로 시간을 재는 것 → DB 구조 파악을 위함
> 

<br/>

**ex)**

1. 공격 대상 : `SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'`
2. 공격 예시 : `SELECT * FROM Users WHERE id = 'abc123' OR (LENGTH(DATABASE())=1 (SLEEP 할 때까지 시도) AND SLEEP(2)) -- INPUT1' AND password = 'INPUT2'`

→ LENGTH는 문자열의 길이를 반환하고 DATABASE는 DB의 이름을 반환함

→ LENGTH(DATABASE()) = 1 이 참이면 SLEEP(2)가 동작함

→ LENGTH(DATABASE()) = n에서 n을 여러 값을 주어 DB의 길이를 알아낼 수 있음 

<br/><br/>

# 6. Stored Procedure SQL Injection

> Stored Procedure : 일련의 쿼리들을 모아 하나의 함수처럼 사용하기 위한 것<br/>
공격에 사용되는 Stored Procedure은 MS-SQL의 xp_cmdshell로 윈도우 명령어를 사용할 수 있게 됨<br/>
공격에 성공한다면 서버에 직접적인 피해를 입힐 수 있음<br/>
> 

<br/><br/>

# 7. Mass SQL Injection

> 기존 SQL Injection과 달리 2008년 발견된 기법으로 한 번의 공격으로 다량의 데이터베이스가 조작되어 큰 피해를 입힘
> 

<br/>

**ex)**

1. 데이터베이스 값을 변조하여 데이터베이스에 악성 스크립트를 삽입
2. 사용자들은 변조된 사이트에 접속 시 좀비 PC로 감염됨
3. 감염된 좀비 PC들은 DDoS 공격에 사용됨

<br/><br/>

# 8. 대응 방안

- 입력값에 대한 검증
- Prepared Statement 사용
- Error Message 노출 금지
- 웹 방화벽 사용
