# 정규화(Normalization)

## A. 정규화란?

> 관계형 데이터베이스 설계에서 중복을 최소화하도록 데이터를 구조화하는 프로세스를 말합니다.

### 목적

- 데이터의 중복을 없애면서 불필요한 데이터를 최소화시킨다.
- 무결성을 지키고, 이상 현상을 방지한다.
- 테이블 구성을 논리적이고 직관적으로 할 수 있다.
- 데이터베이스 구조 확장에 용이해진다.

<br>

### 추가 지식

#### 데이터베이스 무결성이란?

<br>

> 데이터의 정확성, 일관성, 유효성이 유지되는 것

- 정확성: 중복이나 누락이 없는 상태
- 일관성: 원인과 결과의 의미가 연속적으로 보장되어 변하지 않는 상태
- 개체 무결성, 참조 무결성, 도메인무결성 등이 있다.

<br>

#### 이상 현상(Anomaly)

<br>

- 삽입 이상: 불필요한 데이터를 추가해야 삽입할 수 있는 상황 => Insertion Anomaly
- 갱신 이상: 일부만 변경하여 데이터가 불일치하는 모순의 문제 => Update Anomaly
- 삭제 이상: 튜플 삭제로 인해 꼭 필요한 데이터까지 함께 삭제되는 문제 => Deletion Anomaly

<br>

#### 함수적 종속성(Functional Dependency)

<br>

정규화를 위해서는 **속성들 간 관련성**을 파악해야 하는데, 이런 속성들 간의 관련성을 함수적 종속성(Functional Dependency)이라고 한다.
<br>
X의 값을 알면 Y의 값을 바로 식별할 수 있고, X의 값에 Y의 값이 달라질 때, **Y는 X에 함수적 종속**이라고 한다.
X: 결정자, Y: 종속자<br>
X → Y

일반적으로 1개의 릴레이션에는 1개의 함수적 종속성만 존재하도록 정규화한다.

종류

- 완전 함수적 종속성(Full Functional Dependency, 이하 Full FD)
- 부분 함수적 종속성(Partial Functional Dependency, Partial FD)
- 이행적 함수 종속성(Transitive FUnctional Dependency, Transitive FD)

<br>

## B. 제 1 정규형

각 로우마다 컬럼의 값이 1개만 있어야 한다 → 컬럼이 원자값(Atomic Value)를 갖는다.

만족해야 할 조건은 아래와 같다.

- 어떤 릴레이션에 속한 모든 도메인이 원자값만으로 되어 있어야한다.
- 모든 속성에 반복되는 그룹이 나타나지 않는다.
- 기본키를 사용하여 관련 데이터의 각 집합을 고유하게 식별할 수 있어야 한다.

Customer
|Customer ID|First Name|Surname| Telephone Number|
|---|---|---|---|
|123|Robert|Ingram|555-861-2025|
|456|Jane|Wright|555-403-1659, 555-776-4100|
|789|Maria|Fernandez|555-808-9633|

<br>

현재 테이블은 전화번호를 여러 개 가지고 있기 때문에 원자값이 아니다. 따라서 1NF를 충족하게 바꾸면 다음과 같다.

<br>
CustomerName

| Customer ID | First Name | Surname   |
| ----------- | ---------- | --------- |
| 123         | Robert     | Ingram    |
| 456         | Jane       | Wright    |
| 789         | Maria      | Fernandez |

<br>

Customer Telephone Number
|Customer ID|Telephone Number|
|---|---|
|123|555-861-2025|
|456|555-403-1659|
|456|555-776-4100|
|789|555-808-9633|

<br>

## C. 제 2 정규화(2NF)

테이블의 모든 컬럼이 **완전 함수적 종속**을 만족해야 한다.

조금 쉽게 말하면, 테이블에서 기본키가 복합키(키1, 키2)로 묶여있을 때, 두 키 중 하나의 키만으로 다른 컬럼을 결정지을 수 있으면 안된다.

기본키의 부분집합 키가 결정자가 되어선 안된다는 것

<br>
종업원의 기술

| 종업원   | 기술           | 근무지            |
| -------- | -------------- | ----------------- |
| Jones    | Typing         | 114 Main Street   |
| Jones    | Shorthand      | 114 Main Street   |
| Jones    | Whittling      | 114 Main Street   |
| Bravo    | Light Cleaning | 73 Industrial Way |
| Ellis    | Alchemy        | 73 Industrial Way |
| Ellis    | Flying         | 73 Industrial Way |
| Harrison | Light Cleaning | 73 Industrial Way |

- 종업원: 다수의 기술 가지고 있으면서 테이블에 한 차례 이상 나타남 → 후보키 아님
- 기술: 다수의 종업원이 같은 기술 보유하고 있을 때 테이블에 한 차례 이상 나타남 → 후보키 아님
- { 종업원, 기술 }: 유일성과 최소성 만족함 → 후보키🔑

- 남은 속성인 {근무지}는 후보키의 부분집합인 {종업원}에 영향 받음 → 2NF 불충족 ❌

- 이러한 **부분 종속 관계를 제거**하여 제 2 정규형 만족할 수 있도록 만들 수 있다.

<br>

종업원

| 종업원🔑 | 근무지            |
| -------- | ----------------- |
| Jones    | 114 Main Street   |
| Bravo    | 73 Industrial Way |
| Ellis    | 73 Industrial Way |
| Harrison | 73 Industrial Way |

- key: 종업원

종업원의 기술

| 종업원   | 기술           |
| -------- | -------------- | --- |
| Jones    | Typing         |
| Jones    | Shorthand      |
| Jones    | Whittling      |
| Bravo    | Light Cleaning |
| Ellis    | Alchemy        |
| Ellis    | Flying         | 7   |
| Harrison | Light Cleaning |

- key: 종업원, 기술

=> 더 이상 갱신 이상 없다!

<br>

## D. 제 3 정규화(2NF)

2NF가 진행된 테이블에서 이행적 종속을 없애기 위해 테이블을 분리하는 것이다.

> 이행적 종속 : A → B, B → C면 A → C가 성립된다

아래 두가지 조건을 만족시켜야 한다.

- 릴레이션이 2NF에 만족한다.
- 기본키가 아닌 속성들은 기본키에 의존한다.

<br>

대회 우승자

| 대회                 | 연도 | 우승자          | 우승자 생년 월일  |
| -------------------- | ---- | --------------- | ----------------- |
| Des Moines Masters   | 1998 | Chip Masterson  | 14 March 1977     |
| Indiana Invitational | 1998 | Al Fredrickson  | 21 July 1975      |
| Cleveland Open       | 1999 | Bob Albertson   | 28 September 1968 |
| Des Moines Masters   | 1999 | Al Frederickson | 21 July 1975      |
| Indiana Invitational | 1999 | 14 March 1977   |

- key: {대회, 연도}

우승자와 우승자 생년월일이 {대회, 연도} 키에 의해서 결정되므로 2NF 충족. 하지만 우승자와 우승자 생년 월일이 여러 개의 레코드에 반복해서 나타남을 알 수 있다.
이 점이 **갱신 이상**을 불러온다.

- 우승자의 생년 월일 → 우승자: 우승자의 생년 월일은 우승자에 의해 결정(종속적)
- 우승자 → {대회, 연도}: 우승자는 {대회, 연도}에 의해 결정(종속적)
- 우승자의 생년 월일 → {대회, 연도}

3NF를 만들기 위해서는 우승자의 생년 월일을 다른 테이블로 분리해주어야 한다.

<br>

대회 우승자

| 대회                 | 연도 | 우승자          |
| -------------------- | ---- | --------------- |
| Des Moines Masters   | 1998 | Chip Masterson  |
| Indiana Invitational | 1998 | Al Fredrickson  |
| Cleveland Open       | 1999 | Bob Albertson   |
| Des Moines Masters   | 1999 | Al Frederickson |
| Indiana Invitational | 1999 | Chip Masterson  |

- key: 대회, 연도

<br>

우승자 생년 월일

| 우승자         | 우승자 생년 월일  |
| -------------- | ----------------- |
| Chip Masterson | 14 March 1977     |
| Al Fredrickson | 21 July 1975      |
| Bob Albertson  | 28 September 1968 |

- key: 우승자

<br>

## E. 보이스-코드 정규화(BNCF)

릴레이션이 제 3 정규형에 속하고, 함수 종속 관계에서 **모든 종속자가 후보키**인 경우

- X → Y
- X가 테이블의 수퍼키

<br>

Nearest Shops
|Person|Shop type|Nearest shop|
|---|---|---|
|Davidson|Optician|Eagle Eye|
|Davidson|Hairdresser|Snippets|
|Wright|Bookshop|Merlin Books|
|Fuller|Bakery|Doughy's|
|Fuller|Hairdresser|Sweeney Todd's|
|Fuller|Optician|Eagle Eye|

- 후보키
  - {Person, Shop Type}
  - {Person, Nearest Shop}

Nearest shops 테이블의 Person, Shop Type, Nearest Shop 세 계의 속성 모두 후보키에 속하므로 이 테이블은 3NF다. <br>
하지만 `Shop Type`은 수퍼키가 아닌 속성인 `Nearest Shop`에 종속적이므로 BCNF라고 할 수 없다.

이 경우 만약 Eagle Eye가 Fuller 레코드에서 shop type을 "Optometrist"로 변경했지만 "Davidson" 레코드에는 제대로 반영되지 않을 수 있다.

1. 릴레이션에서 BCNF를 위반하는 함수적 종속성을 찾는다 (Shop Type → Nearest shop)
2. 릴레이션을 위반하는 함수적 종속성에 해당하는 애트뷰트들만 따로 릴레이션을 만든다(EX. R={shop, shop type})
3. 릴레이션에 남아있는 애트리뷰트와 함수적 종속성 화살표 왼쪽에 있는 애트리뷰트를 한 애트리뷰트로 한다(R={shop, person})

<br>

Shop near person
|Person|Shop|
|---|---|
|Davidson|Eagle Eye|
|Davidson|Snippets|
|Wright|Merlin Books|
|Fuller|Doughy's|
|Fuller|Sweeney Todd's|
|Fuller|Eagle Eye|

- 후보키: {Person, Shop}

Shop
|Shop|Shop Type|
|---|---|
|Eagle Eye|Optician|
|Snippets|Hairdresser|
|Merlin Books|Bookshop|
|Doughy's|Bakery|
|Sweeney Todd's|Hairdresser|

- 후보키: {Shop}

## F. 참고자료

🔗 https://gyoogle.dev/blog/computer-science/data-base/Normalization.html

🔗 https://ko.wikipedia.org/wiki/%EC%A0%9C2%EC%A0%95%EA%B7%9C%ED%98%95

🔗 https://en.wikipedia.org/wiki/Boyce%E2%80%93Codd_normal_form#Achievability_of_BCNF
