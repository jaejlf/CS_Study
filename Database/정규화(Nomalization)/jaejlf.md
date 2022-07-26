# 📍 데이터베이스 정규화

관계형 데이터베이스의 설계에서 `중복을 최소화`하게 데이터를 구조화하는 프로세스

- 기본 정규형 : 제 1 정규형, 제 2 정규형, 제 3 정규형, BCNF
- 고급 정규형 : 제 4 정규형, 제 5 정규형
- 목적
  1. 중복을 배제하여 삽입/삭제/갱신 이상의 발생을 방지
  2. 각 릴레이션에 중복된 종속성을 여러 개의 릴레이션에 분할
  3. 어떠한 릴레이션이라도 데이터베이스 내에서 표현 가능하게 함
  4. 데이터 삽입 시 릴레이션을 재구성할 필요성 감소
  5. 효과적인 검색 알고리즘 생성 가능

<br>

## 1NF (제 1 정규형)

- 릴레이션에 속한 모든 속성의 도메인이 `더이상 분해되지 않는 원자값으로만 구성`된 정규형
- 각 로우마다 컬럼의 값이 1개씩만 존재해야한다 => `모든 컬럼이 원자값`을 가져야한다.

<br>

### 1NF 이전

![image](https://user-images.githubusercontent.com/78673570/185756284-f17ce61a-4fba-440b-a6f1-136afa741e31.png)

- '수강과목' 컬럼의 속성이 원자값이 아니었다.
- 갱신/삭제 이상이 발생할 수 있다. (ex. '홍길동'이 '국어' 과목 수강 취소할 경우, '영어' 과목까지 수강 취소)

<br>

### 1NF 이후

![image](https://user-images.githubusercontent.com/78673570/185756323-f1b5d24d-52dc-4815-ac39-d68a71be0546.png)

- 모든 컬럼이 원자값을 가진다.
- 데이터의 중복은 더 증가했다. (데이터의 논리적 구성을 위해 이 부분은 희생)

<br>

## 2NF (제 2 정규형)

- 테이블의 모든 컬럼이 `완전 함수 종속`을 만족하는 정규형
- 기본키 중에 특정 컬럼에만 종속된 컬럼(= 부분적 종속)이 없어야 한다.
- `부분 함수 종속을 제거`해야 한다.

    > - 완전 함수 종속 : 어떤 속성이 기본키에 대해 완전히 종속일 때
    > - 부분 함수 종속
    >   - 어떤 속성이 기본키가 아닌 다른 속성에 종속되었을 때
    >   - 기본키가 복합키일 경우, 기본키를 구성하는 속성 중 일부에게만 종속된 경우

<br>

### 2NF 이전

![image](https://user-images.githubusercontent.com/78673570/185756488-d2ab27da-c8fe-46f9-bcd0-57008cf6f923.png)

- 기본키는 (이름, 수강과목)으로, '이름'과 '수강과목'이 모두 있어야 한 로우를 구분할 수 있다.
- 그런데 '나이'의 경우 '이름'에만 종속되어 있다. => 부분 함수 종속 !
- 삽입/갱신/삭제 이상이 발생할 수 있다. (ex. 수강신청을 할 때, 불필요한 '나이' 정보까지 계속해서 중복 적재)

<br>

### 2NF 이후

![image](https://user-images.githubusercontent.com/78673570/185756562-1aeb0052-cd8e-47f3-8be8-ef5ba18f2e39.png)

- 두 개의 테이블로 분리하여, 각각의 테이블의 모든 컬럼이 완전 함수 종속을 만족한다.
- 삽입/갱신/삭제 문제를 겪지 않을 수 있다. (그러나 더 복잡한 테이블의 경우 이상이 발생할 수 있다.)

<br>

## 3NF (제 3 정규형)

- 기본키를 제외한 속성들 간의 `이행적 함수 종속`이 없는 정규형
- 기본키 이외의 다른 컬럼이 그 외 다른 컬럼을 결정할 수 없다.

    > 이행적 함수 종속 : A → B이고, B → C일 때, A → C인 관계

<br>

### 3NF 이전

![image](https://user-images.githubusercontent.com/78673570/185756691-9fd5d44a-04a2-466f-b31e-8bae70902309.png)

- 이행적 함수 종속 관계가 성립한다.
- '홍길동 → 컴퓨터', '컴퓨터 → 공대' 일 때, '홍길동 → 공대'인 관계가 성립한다.
- 삽입/갱신/삭제 이상이 발생할 수 있다. (ex. '홍길동'이 자퇴할 경우, '컴퓨터'학과 정보도 삭제)

<br>

### 3NF 이후

![image](https://user-images.githubusercontent.com/78673570/185756922-0d84be8d-1cfb-416a-88d6-50e3e10317f3.png)

- 데이터가 논리적인 단위(학생, 대학)으로 분리되었다.
- 데이터의 중복이 감소했다.

<br>

## BCNF (Boyce and Codd Normal Form)

- 모든 결정자가 `후보키 집합에 속하는` 정규형
- 3NF 보다 좀 더 엄격한 제약조건을 제시한 정규형
- `후보키가 아닌 결정자를 제거`해야 한다.

<br>

### BCNF 이전

![image](https://user-images.githubusercontent.com/78673570/185757565-0ffc3593-d10c-440b-bbbe-d2408b699274.png)

- 삽입/삭제/갱신 이상이 발생할 수 있다. (ex. '홍길동'이 '데이터베이스' 과목을 수강 취소하면, '김교수'가 '데이터베이스' 과목을 담당한다는 정보도 삭제)
- (이름, 과목), (이름, 교수)가 후보키가 되고, '교수'만으로는 후보키가 될 수 없다.
- 그러나 '교수'는 후보키가 아님에도 '과목'을 결정할 수 있기 때문에 후보키가 아닌 결정자이다.

<br>

### BCNF 이후

![image](https://user-images.githubusercontent.com/78673570/185758028-32673b46-ace7-4a2c-991e-cd67750826e7.png)

- '이름-교수' 릴레이션은 함수 종속 관계가 성립하지 않는 동등한 '이름', '교수' 속성으로 구성되어 있고, (이름, 교수)가 기본키를 담당한다. 즉, 후보키가 아닌 결정자가 존재하지 않기 때문에 BCNF이다.
- '교수-과목' 릴레이션은 교수와 과목이 함수 종속 관계이며, (교수)가 유일한 후보키이자 기본키이다. 즉, 후보키가 아닌 결정자가 존재하지 않기 때문에 BCNF이다.

<br>

.
<br>
.

=> 일반적으로 제 3 정규형이나 BCNF에 속하도록 분해한다 ! (무조건 제 4, 5 정규형에 속하도록 해야하는 것은 아님.)

<br>

## 4NF

릴레이션이 `BCNF를 만족`하면서, 함수 종속이 아닌 `다치 종속(MVD: Multi Valued Dependency)을 제거`해야 만족할 수 있다.

<br>

### 다치 종속

- 릴레이션의 속성 X, Y, Z가 있을 때, Y와 Z는 서로 독립적이지만 Y와Z가 X에 종속적이고 여러개의 값이 허용될때 발생
- `X ->> Y`, `X ->> Z`로 표기
- 컬럼의 속성값에 집합을 허용하지 않는 1NF의 제약으로 인해 발생
- 하나의 속성이 여러 개의 값을 결정하면 이것을 `다치 결정`한다고 한다.
- ex.
  - '수강과목'과 '동호회'는 서로 독립적이지만, '학생'에 종속되어 있으며 여러 개의 값이 허용된다.
  - 따라서 '수강과목'과 '동호회'는 학생에 `다치 종속` 되어 있다. (학생 ->> 수강과목, 학생 ->> 동호회)

<br>

## 5NF

릴레이션이 `4NF를 만족`하면서, 후보키를 통하지 않는 `조인 종속(JD: Join Dependency) 을 제거`해야 만족할 수 있다. (조인 종속이 존재하는 릴레이션이 사용하기 편리하다. 지나치게 이상적인 정규형)

<br>

### 조인 종속

- 릴레이션을 여러 개의 릴레이션으로 분해하였다가, 다시 조인하여 복원할 수 있다면 `조인 종속성`을 가진다.

<br><br>

# 📍 정리

정규화 | 개념 | 제거 대상
:--: | -- | --
1NF | 모든 컬럼이 `원자값`인 정규형 | 모든 컬럼이 원자값을 가지도록 분해
2NF | 모든 컬럼이 `완전 함수 종속`을 만족하는 정규형 | 부분 함수 종속을 제거
3NF | 기본키를 제외한 속성들 간의 `이행적 함수 종속`이 없는 정규형 | 이행적 함수 종속 제거
BCNF | 모든 결정자가 `후보키 집합에 속하는` 정규형 | 후보키가 아닌 결정자 제거
4NF | `다치 종속이 제거`된 정규형 | 다치 종속 제거
5NF | `조인 종속이 제거`된 정규형 | 조인 종속 제거
