# 💡 Key

## 정의

키(Key)란, 데이터베이스에서 조건에 만족하는 튜플을 찾거나(검색) 순서대로 정렬할 때 다른 튜플들과 구별할 수 있는 기준이 되는 Attribute(속성)을 말한다.

<br/>

## 종류

![image](https://user-images.githubusercontent.com/75151848/185210079-7287b6f6-9135-47e2-a05d-dfd06037d5ac.png)

### 1️⃣ Super Key (슈퍼 키)

유일성을 만족하는 키

<br/>

### 2️⃣ Candidate Key (후보 키)

유일성과 최소성을 만족하는 키

기본키가 될 수 있는 후보이기 때문에 후보키라고 불린다.

<br/>

### 3️⃣ Primary Key (기본 키)

후보키에서 선택된 키

- NULL 값을 가질 수 없다. (`NOT NULL`)
- 중복된 값을 가질 수 없다. (`UNIQUE`)

#### PK 설정 방법1 (컬럼 레벨)

```sql
CREATE TABLE 테이블이름 (
	필드이름 필드타입 PRIMARY KEY,
	...
)
```

#### PK 설정 방법2 (테이블 레벨)

```sql
CREATE TABLE 테이블이름(
	필드이름 필드타입,
	...,
	[CONSTRAINT 제약조건이름] PRIMARY KEY (필드이름)
)
```

<br/>

### 4️⃣ Alternate Key (대체 키)

후보 키 중에 기본 키로 선택되지 않은 키

<br/>

### 5️⃣ Foreign Key (외래 키)

어떤 테이블(Relation) 간의 기본 키(Primary key)를 참조하는 속성

테이블(Relation)들 간의 관계를 나타내기 위해서 사용된다.

`자식 테이블`: 외래키가 포함된 테이블  
`부모 테이블`: 외래키 값을 제공하는 테이블

#### FK 설정 방법1 (컬럼 레벨)

```sql
CREATE TABLE 테이블이름(
	필드이름 필드타입 [CONSTRAINT 제약조건이름] 
		REFERENCES 참조테이블이름(참조필드이름)
		[ON DELETE CASCADE | ON DELETE SET NULL],
	...
)
```

#### FK 설정 방법2 (테이블 레벨)

```sql
CREATE TABLE 테이블이름(
	필드이름 필드타입,
	...,
	[CONSTRAINT 제약조건이름] FOREIGN KEY (필드이름) 
		REFERENCES 참조테이블이름(참조필드이름)
		[ON DELETE CASCADE | ON DELETE SET NULL]
)
```

<br/>

## 📌  참고

- [https://inpa.tistory.com/entry/DB-📚-키KEY-종류-🕵️-정리](https://inpa.tistory.com/entry/DB-%F0%9F%93%9A-%ED%82%A4KEY-%EC%A2%85%EB%A5%98-%F0%9F%95%B5%EF%B8%8F-%EC%A0%95%EB%A6%AC)
- [https://velog.io/@hoha/DB-KEY의-종류-정규화-반정규화](https://velog.io/@hoha/DB-KEY%EC%9D%98-%EC%A2%85%EB%A5%98-%EC%A0%95%EA%B7%9C%ED%99%94-%EB%B0%98%EC%A0%95%EA%B7%9C%ED%99%94)
- [https://lipcoder.tistory.com/438](https://lipcoder.tistory.com/438)
