# 📍 SQL Injection

- 해커에 의해 조작된 SQL 쿼리문이 데이터베이스에 그대로 전달되어 비정상적 명령을 실행시키는 공격
- 공격이 비교적 쉬운 편이고, 공격에 성공할 경우 큰 피해를 입힐 수 있는 공격

<br><br>

# 📍 공격 방법

## Error Based SQL Injection

![image](https://user-images.githubusercontent.com/78673570/185746252-f2205693-c0c1-404c-bbe5-0a8fcae3de8e.png)

- 논리적 오류를 이용한 SQL 인젝션
- 해커는 `OR 1=1 --`을 입력하여, WHERE절을 모두 참으로 만들고 그 이후에 주석(`--`)을 넣어 뒤의 구문을 모두 주석 처리
- 가장 많이 쓰이고, 대중적인 방법

<br>

## Union Based SQL Injection
  
![image](https://user-images.githubusercontent.com/78673570/185746289-97b317f8-3303-46ba-bb36-6ae348695ab0.png)

- 2개 이상의 쿼리를 요청하여 결과를 얻어내는 UNION 연산자를 이용한 공격 기법
- 정상적인 쿼리문에 하나의 추가 쿼리를 삽입하여 원하는 정보를 획득
- Union Injection이 성공하기 위해서는 `Union 하는 두 테이블의 컬럼 수가 같아야` 하고, `데이터형이 같아야`한다.
- UNION 키워드와 함께 컬럼 수를 맞춰서 SELECT 구문을 넣어주면, 두 쿼리문이 합쳐져서 하나의 테이블로 보여진다.

<br>

## Blind Based SQL Injection

에러가 발생되지 않는 사이트에서는 ErrorBased, Union Based 기법을 사용할 수 없기 때문에, Blind Based 기법을 통해 정상적인 쿼리가 수행되는지를 판단

<br>

### Boolean Based SQL

![image](https://user-images.githubusercontent.com/78673570/185748570-edd8ffeb-6147-4ae5-9868-d3685d7ca546.png)

- 서버가 응답하는 참/거짓만으로 데이터를 얻어내는 공격 기법
- 쿼리를 삽입했을 때 쿼리의 참/거짓에 대한 반응을 구분할 수 있을 때 사용
- DB 테이블명, 버전 등을 알아내기 위해 사용
- 수백 수천 번의 시도를 해야 하기 때문에, 보통 자동화 프로그램을 이용하여 시도

<br>

### Time Based SQL

![image](https://user-images.githubusercontent.com/78673570/185747384-c7e54c7a-7f4d-48db-ab0b-d59ee318fd3b.png)

- 참/거짓의 응답 결과가 같을 때 시간을 지연시키는 쿼리를 주입하여 시간 차이로 참/거짓 여부를 판단
- 궁극적으로는 DB 구조를 파악하기 위함

<br><br>

# 📍 방어 방법

## 입력 값에 대한 검증

- 사용자의 입력이 DB의 쿼리에 동적으로 영향을 주는 경우, 입력된 값이 개발자가 의도한 값인지 검증
- ex. 특수문자, 공백, SQL 명령어(UNION, SELECT, ...) 등 필터링

<br>

## 저장 프로시저 사용

```sql
# Statement
String query = "select * from table where id=" + id; -- id 값에 따라 쿼리 구조가 변경될 수 있다.

↓

# Prepared Statement
String query = "select * from table where id=?"; -- id 값에 관계없이 쿼리 구조는 정해져있다.
```
Prepared Statement는 사용자의 입력값이 DB의 파라미터로 들어가기 전에, DBMS가 미리 컴파일하여 실행하지 않고 대기한다. 따라서 지정된 형식의 데이터가 아니면 쿼리가 실행되지 않기 때문에 보안성을 크게 향상시킬 수 있다.

<br>

### 💡 Statement vs Prepared Statement

쿼리는 DBMS 내부적으로 ↓ 4가지 과정(parse, bind, execute, fetch) ↓ 을 거쳐 결과를 출력한다.

![image](https://user-images.githubusercontent.com/78673570/185748306-4b214351-caee-4427-8806-46c6c8270bbf.png)

<br>

parse 과정을 거친 후에 생성되는 결과를 파싱하여 ↓ 트리를 생성 ↓ 하고, 필요할 때마다 꺼내서 사용한다. 반복적으로 트리를 사용하기 위해서 자주 변경되는 부분을 변수로 선언해두고, 매번 다른 값을 `바인딩`하여 사용한다.

![image](https://user-images.githubusercontent.com/78673570/185748158-2cb21a0e-d022-4b03-817f-d3b1b6dd4b1f.png)

<br>

- 일반적인 `Statement`는 매번 parse 부터 fetch까지 모든 과정을 수행한다. (= `Hard Parsing`)
- `Prepared Statement`는 효율을 높이기 위해 parse 과정을 최초 1번만 수행하고 그 이후는 생략할 수 있다. (= `Soft Parsing`)
- `Prepared Statement`에서 `바인딩` 변수를 사용하였을 때, 쿼리의 문법 처리 과정이 미리 수행되기 때문에, 바인딩 데이터는 SQL 문법적인 의미를 가질 수 없다. 따라서 SQL Ingection을 원천적으로 봉쇄할 수 있다.

<br>

## 서버 보안

- 최소 권한 유저로 DB 운영
- 사용하지 않는 저장 프로시저와 내장 함수 제거 또는 권한 제어
- 목적에 따라 쿼리 권한 수정
- 공용 시스템 객체의 접근 제어
- 신뢰할 수 있는 네트워크/서버에 대해서만 접근 허용
- 에러 메세지 노출 차단
