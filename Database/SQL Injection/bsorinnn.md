# SQL Injection

<br>

> 악의적인 사용자가 보안상의 취약점을 이용하여, 임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위

<br>

인젝션 공격은 OWASP Top 10에 속해 있으며, 공격이 비교적 쉬운 편이고 공격에 성공할 경우 큰 피해를 입힐 수 있습니다.

<br>

(\* OWASP - Open Web Application Security Project에 따라 악용가능성, 탐지가능성 및 영향에 대해 빈도수가 높고 보안상 영향을 크게 줄 수 있는 10가지 웹 애플리케이션 보안 취약점 목록. )

## A. 공격 종류 및 방법

인젝션 공격은 주로 로그인과 같이 유저에게 항목을 입력을 받을 때 일어납니다. 사용자의 입력값과 함께 임의의 SQL 구문이 주입되고 관리자가 모르게 실행됩니다.

<br>

다음은 유저에게서 유저 아이디를 입력받아 유저를 찾는 SQL문입니다. 이렇게 SQL 문에 유저 인풋을 사용할 경우 일어날 수 있는 인젝션 공격을 알아보겠습니다.

<br>

```SQL
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = " + txtUserId;
```

<br>

### Error based SQL Injection

#### 1. SQL Injection Based on 1=1 is Always True

```SQL
SELECT * FROM Users WHERE UserId = 105 OR 1=1;
```

OR 1=1은 언제나 참(`TRUE`)이기 때문에 상위 SQL문으로는 `Users` 테이블의 모든 정보를 조회할 수 있게 됩니다.

특히 `Users` 테이블이 사용자의 비밀번호나 개인 정보가 담겨 있다면 위험성이 더 커집니다.

<br>

#### 2. SQL Injection Based on ""="" is Always True

다음은 유저가 로그인을 할 때의 예시입니다.

```SQL
uName = getRequestString("username");
uPass = getRequestString("userpassword");

sql = 'SELECT * FROM Users WHERE Name ="' + uName + '" AND Pass ="' + uPass + '"'
```

RESULT

```SQL
SELECT * FROM Users WHERE Name ="John Doe" AND Pass ="myPass"
```

사용자의 입력에 따라 상단과 같은 SQL 문이 실행된다고 할 때,악의적인 사용자는 유저의 이름과 비밀번호 입력창에 " 나 ""="를 넣음으로써 정보에 접근할 수 있습니다.

<br>

```SQL
SELECT * FROM Users WHERE Name ="" or ""="" AND Pass ="" or ""=""
```

그런 경우 위와 같은 SQL 문이 실행되고, 이는 `Users` 테이블의 모든 정보를 리턴합니다.
`OR ""=""` 가 언제나 참(`TRUE`)이기 때문입니다.

<br>

### Union Based SQL Injection

- SQL에서 `Union` 키워드 : 두 개의 쿼리문에 대한 결과를 통합하여 하나의 테이블로 보여준다.
  - (실행 조건)
  1. Union하는 테이블의 컬럼 수가 같아야 한다
  2. 데이터 타입이 같아야 한다

실행하려는 SQL문

- `Board` 테이블에서 게시글 검색 SQL
- 입력값을 `title`이나 `contents`의 데이터와 비교, 비슷한 글자 있는 데이터 출력

```SQL
SELECT * FROM BOARD WHERE title LIKE `%INPUT%` OR contents `%INPUT%`
```

SQL Injection

- 사용자의 id와 password를 요청

```SQL
UNION SELECT null, id, password FROM User
```

최종 실행되는 SQL문

```SQL
SELECT * FROM BOARD WHERE title LIKE `%INPUT%` OR contents `%INPUT%` UNION SELECT null, id, password FROM User
```

입력값으로 Union 키워드와 함께 컬럼 수를 맞춰서 SELECT 구문을 넣어주게 되면 두 쿼리문이 합쳐서서 하나의 테이블로 보여지게 됩니다. <br>

=> 인젝션이 성공하게 되면, 사용자의 개인정보가 게시글과 함께 화면에 보여지게 됩니다.

<br>

### Blind SQL Injection

<br>

#### 1. Boolean based SQL

<br>
Blind SQL Injection?<br>
데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고, 단순히 참과 거짓의 정보만 알 수 있을 때 사용

<br>

로그인 폼에 SQL Injection이 가능하다고 가정했을 때, 서버가 응답하는 로그인 성공과 로그인 실패 메시지를 이용하여, DB의 테이블 정보 등을 추출해 낼 수 있습니다.

실행하려는 SQL문

```SQL
SELECT * FROM Users WHERE id = 'INPUT1' AND passsword = 'INPUT2'
```

SQL Injection

(MySQL인 경우)

- MySQL 에서 테이블 명을 조회하는 구문으로 limit 키워드를 통해 하나의 테이블만 조회하고, SUBSTR 함수로 첫 글자만, 그리고 마지막으로 ASCII 를 통해서 ascii 값으로 변환
- 만약 조회되는 테이블 명이 `Users`라면 ‘U’ 자가 ascii 값으로 조회가 될 것이고, 뒤의 100 이라는 숫자 값과 비교
- 거짓이면 로그인 실패

```SQL

-
abc123 and ASCII(SUBSTR(SELECT name FROM information_schema.tables WHERE table_type = 'base table' limit 0,1)1,1) > 100 --
```

최종 실행되는 SQL문

- Blind Injection을 이용하여 데이터베이스의 테이블 명 알아냄

```SQL
SELECT * FROM Users WHERE id = 'abc123' and ASCII(SUBSTR(SELECT name FROM information_schema.tables WHERE table_type = 'base table' limit 0,1)1,1) > 100 --
```

인젝션이 가능한 로그인 폼을 이용하여 악의적인 사용자는 임의로 가입한 abc123이란 아이디와 함께 SQL 문을 주입합니다. <br>
해당 SQL문은 MySQL에서 테이블명을 조회하는 구문입니다. 거짓이면 로그인 실패가 되고, 참이 될 때까지 뒤의 숫자 `100` 을 변경하면 됩니다.

=> 위의 방법을 통하여 단기간 내에 테이블 명을 알아낼 수 있습니다.

<br>

#### 2. Time Based SQL

서버로부터 특정한 응답 대신 참 또는 거짓의 정보를 통하여 데이터베이스의 정보 유츄

사용되는 함수: (MYSQL기준) `SLEEP` ,
`BENCHMARK`

<br>

실행하려는 SQL문

```SQL
SELECT * FROM Users WHERE id = 'INPUT1' AND passsword = 'INPUT2'
```

<br>

SQL Injection

- LENGTH: 문자열의 길이 반환
- DATABASE: 데이터베이스의 이름 반환

```SQL
abc123 OR (LENGTH(DATABASE())=1 AND SLEEP(2))

```

<br>

최종 실행 SQL문

```SQL
SELECT * FROM Users WHERE id = 'abc123' OR (LENGTH(DATABASE())=1 AND SLEEP(2))
```

주입된 구문에서 LENGTH(DATABASE()) = 1 가 참이면 SLEEP(2) 가 동작하고, 거짓이면 동작하지 않습니다.<br>
따라서 1 숫자를 조작하여 데이터베이스의 길이를 알아낼 수 있습니다.

`BENCHMARK`나 `WAIT` 도 비슷하게 사용할 수 있습니다.

<br>

### Store Procedure SQL Injection

<br>

- 저장된 프로시져(store procedure): 일련의 쿼리들을 모아 하나의 함수처럼 사용하기 위한 것
  - 공격에 사용되는 대표적인 저장된 프로시져: MS-SQL 에 있는 xp_cmdshell
    - 윈도우 명령어 사용 가능
- 공격자가 시스템 권한을 획득해야 하므로 공격 난이도가 높습니다.
- 그러나 성공 시 서버에 직접적인 피해 입힐 수 있습니다.

<br>

### MASS SQL Injection

- 기존 SQL과 달리 한번의 공격으로 다량의 데이터베이스가 조작되어 큰 피해를 입히는 것
- 2008년에 처음 발견됨
- MS-SQL을 사용하는 ASP 기반 웹 애플리케이션에서 많이 사용
- 쿼리문을 HEX 인코딩 방식으로 인코딩 하여 공격
- 데이터베이스 값을 변조하여 데이터베이스에 악성스크립트를 삽입하고, 사용자들이 변조된 사이트에 접속 시 좀비PC로 감염
  - 감염된 좀비 PC는 DDos 공격에 사용

<br>

## B. 대응 방안

<br>

### 입력 값에 대한 검증

서버 단에서 화이트리스트 기반으로 검증해야 합니다.

<br>

(\*화이트리스트 - '안전'이 증명된 것만을 허용하는 것으로 '악의성'이 입증된 것을 차단하는 블랙리스트 보안과 상반되는 보안 방식.)

출처: https://sugerent.tistory.com/135 [MISTERY:티스토리]

<br>

### Prepared Statement 구문사용

사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에 DBMS가 미리 컴파일 하여 실행하지 않고 대기합니다. <br>
그 후 사용자의 입력 값을 문자열로 인식하게 하여 공격쿼리가 들어간다고 하더라도, 사용자의 입력은 이미 의미 없는 단순 문자열 이기 때문에 전체 쿼리문도 공격자의 의도대로 작동하지 않습니다.

<br>

### Error Message 노출 금지

공격자가 SQL Injection을 실행하기 위해서는 데이터베이스의 정보(이름, 컬럼명) 등이 필요합니다.
<br>
데이터베이스 에러 발생 시 따로 처리를 해주지 않았다면, 에러가 발생한 쿼리문과 함께 에러에 관한 내용을 반환헤 줍니다. 여기서 테이블명 및 컬럼명 그리고 쿼리문이 노출이 될 수 있기 때문에, 데이터 베이스에 대한 오류발생 시 사용자에게 보여줄 수 있는 페이지를 제작 혹은 메시지박스를 띄우도록 하여야 합니다.

<br>

## C. 참고자료

🔗 https://www.w3schools.com/sql/sql_injection.asp

🔗 https://noirstar.tistory.com/264

🔗 https://gyoogle.dev/blog/computer-science/data-base/SQL%20Injection.html
