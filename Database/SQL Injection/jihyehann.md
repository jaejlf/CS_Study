# 💡 SQL Injection
## 1. 정의
SQL Injection (SQL 삽입 공격)이란, 응용 프로그램의 보안 취약점을 이용해서 악의적인 SQL 구문을 삽입, 실행시켜서 데이터베이스에서 정보를 탈취하거나 조작하는 행위를 말한다.

<br/>

## 2. 공격 유형

### 1) Form SQL Injection

Html Form 기반 인증을 담당하는 애플리케이션의 취약점이 있는 경우, 사용자 인증을 위한 쿼리문의 조건을 임의로 조작하여 인증을 우회하는 기법이다.

![image](https://velog.velcdn.com/images/wisdom-one/post/b9fc6a2d-48b7-4a85-aca0-4f079eee3561/image.png)

로그인 로직에서 회원의 id와 password가 일치하는지 검사하는 조건문에 `'OR 1=1--` 을 입력하여 조건이 항상 참이 되도록 하면 로그인에 성공하게 된다.

<br/>

### 2) Error-Based SQL Injection

DB 쿼리에 대한 `에러값`을 기반으로 한 단계씩 점진적으로 DB 정보를 획득할 수 있는 기법이다.

> Error-Based SQL Injection에 관한 예시는 [여기](https://byounghee.tistory.com/148#:~:text=1\)%20%EC%97%90%EB%9F%AC%20%EB%A9%94%EC%8B%9C%EC%A7%80%EB%A5%BC%20%ED%86%B5%ED%95%9C%20DB%20%EC%A0%95%EB%B3%B4%ED%99%95%EC%9D%B8)에 잘 정리되어 있다.

<br/>

### 3) Union SQL Injection

`union select 쿼리` 를 이용하여 한 쿼리의 결과를 다른 쿼리의 결과에 결합하여 공격하는 기법이다.

<br/>

### 4) Blind SQL Injection

DB 쿼리에 대한 오류 메시지를 반환하지 않으면 공격을 할 수 없는 Error-Based SQL Injection과 달리 오류 메시지가 아닌 `쿼리 결과의 참과 거짓` 을 통해 의도하지 않은 SQL문을 실행함으로써 데이터베이스를 비정상적으로 공격하는 기법이다.

<br/>

### 5) Mass SQL Injection

기존 SQL Injection의 확장된 개념으로, 한 번의 공격으로 대량의 DB 값이 변조되어 홈페이지에 치명적인 영향을 미치는 공격 기법이다.

<br/>

### 6) Stored Procedure SQL Injection

저장 프로시저(Stored Procedure)를 이용하여 공격하는 기법이다.

<br/>

## 3. 대응 방안

### 1) 입력값 검증

사용자의 입력이 DB Query 에 동적으로 영향을 주는 경우, 입력된 값이 개발자가 의도한 값(요효값)인지 검증해야 한다.

이때 블랙리스트 방식(특수문자인지, 불필요한 문자 체크)이 아닌 화이트리스트(영어,숫자인지 체크)를 권장한다.
블랙리스트 방식으로는 체크할 것이 무궁무진하게 많이 때문에 입력받은 값이 자신이 생각한 데이터가 맞는지 체크하는 방식이 더 효율적이다.

<br/>

### 2) Prepared Statement 구문사용

`Prepared Statement` 구문을 사용하게 되면, 사용자의 입력값이 데이터베이스의 파라미터로 들어가기 전에 DBMS가 미리 컴파일하여 실행하지 않고 대기한다. 
이후 사용자의 입력값을 문자열로 인식하게 하여 공격 쿼리가 들어간다고 하더라도, 사용자의 입력은 이미 의미없는 단순 문자열이기 때문에 공격자의 의도대로 작동하지 않는다.

<br/>

### 3) Error Message 노출 금지

데이터베이스 에러 발생 시 처리를 해주지 않았다면, 에러가 발생한 쿼리문과 함께 에러에 관한 내용을 반환하게 된다.
반환되는 내용은 공격자가  SQL Injection을 수행하기 위해서 필요한 정보(테이블명, 컬럼명 등)을 포함하고 있으므로, 오류 내용을 그대로 출력해서는 안 된다.

에러 메시지는 정해진 사용자에게 유용한 최소한의 정보만을 표현해야 하며, 예외 사항은 내부적으로 처리하고 오류 정보를 출력하는 것은 금지해야 한다.




<br/><br/>

## 🔖 참고
- NCS 정보처리기술사 연구회 외, 『수제 정보처리기사 필기 2권』, 건기원(2022), p88-91
- https://byounghee.tistory.com/148
- https://noirstar.tistory.com/264
- http://blog.plura.io/?p=6056
- https://rh-cp.tistory.com/70


