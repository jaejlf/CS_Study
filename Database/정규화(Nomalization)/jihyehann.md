# 💡 정규화(Normalization)	
## 1. 정의

### Normalization

관계형 데이터 모델에서 **데이터의 중복성을 제거**하여 이상 현상(Anomaly)을 방지하고, 데이터의 일관성과 정확성을 유지하기 위해 무손실 분해하는 과정을 말한다.

> #### 💡 이상 (Anomaly)
> 정규화를 거치지 않은 데이터베이스 내에 데이터들이 불필요하게 중복되어 릴레이션 조작 시 발생하는 예기치 않은 현상을 말한다.
>
> 삽입 이상(Insertion Anomaly), 삭제 이상(Deletion Anomaly), 갱신 이상(Update Anomaly)이 있다.

<br/>

## 2. 목적

- 중복 데이터를 최소화하여 테이블 불일치 위험을 최소화한다.
- 수정, 삭제 시 이상 현상을 방지함으로써 데이터 구조의 일관성을 최대화한다.
- 데이터 삽입 시 릴레이션의 재구성에 대한 필요성을 줄인다.
- 효과적인 검색 알고리즘을 생성할 수 있다.

<br/>

## 3. 정규화 단계

![](https://velog.velcdn.com/images/wisdom-one/post/43aef4a5-c911-4217-a921-3b0934088326/image.png)


### 1) 제 1정규화 (1NF)

**" 테이블 내의 속성값은 `원자값`을 가지고 있어야 한다. "**

1NF는 다음을 만족해야 한다.

1. 각 컬럼이 하나의 속성만을 가져야 한다.
2. 하나의 컬럼은 같은 종류나 타입(type)의 값을 가져야 한다.
3. 각 컬럼이 유일한(unique) 이름을 가져야 한다.
4. 칼럼의 순서가 상관없어야 한다.

<br/>

### 2) 제 2정규화 (2NF)

**" `부분 함수 종속`을 제거한다. (완전 함수 종속 관계)"**

2NF는 다음을 만족해야 한다.

1. 제 1정규형을 만족해야 한다.
2. 모든 컬럼이 부분적 종속이 없어야 한다. 즉, 모든 컬럼이 완전 함수 종속을 만족해야 한다.


> #### 💡 부분 함수 종속 (Partial Functional Dependency) 
> 기본키 중에 특정 컬럼에만 종속되는 것을 말한다.
>
> #### 💡 완전 함수 종속 (Full Functional Dependency)
> 기본키의 부분집합이 결정자가 되어선 안 된다는 것이다.

<br/> 

#### 예시

<img style="margin-top:0" src="https://velog.velcdn.com/images/wisdom-one/post/287cc94a-aed1-42f2-b9a5-aaa64c62e9be/image.png" />

(학생번호, 과목) 복합키가 기본키라고 하자.  

이때 특정 과목의 지도교수는 과목명만 알면 알 수 있다.   

즉, 지도교수 컬럼이 (학생번호, 과목)에 종속되지 않고 (과목)에만 종속적이다. 

<br/> 

제 2 정규화를 통해 다음과 같이 분리해야 한다.

<img style="margin-top:0" src="https://velog.velcdn.com/images/wisdom-one/post/7dfb58dc-70d9-4fea-8663-823c6e165cc2/image.png"/>


<br/>

### 3) 제 3정규화 (3NF)

**" `이행 함수 종속`을 제거한다. "**

3NF는 다음을 만족해야 한다.

1. 제 2정규형을 만족해야 한다.
2. 기본키를 제외한 속성들간의 이행 종속성 (Transitive Dependency)이 없어야 한다.

> #### 💡 이행 함수 종속 (Transitive Functional Dependency)
> `A → B`, `B → C` 일 때 `A → C` 를 만족하면 이행 함수 종속이라고 한다. 

<br/> 

#### 예시

<img style="margin-top:0" src="https://velog.velcdn.com/images/wisdom-one/post/1953d93d-5120-4d71-af80-4bd6b3f350df/image.png"/>

`ID → 등급`, `등급 → 할인율`, `ID → 할인율` 을 만족한다. 즉 이행 함수 종속이 존재한다.  

<br/> 

제 3 정규화를 통해 다음과 같이 분리해야 한다.

<img style="margin-top:0" src="https://velog.velcdn.com/images/wisdom-one/post/7f0bfbd9-46da-429c-bf07-60c66642bd02/image.png"/>


<br/>

### 4) 보이스-코드 정규화 (BCNF)

**" 결정자가 후보키가 아닌 함수 종속을 제거한다. "**

BCNF는 다음을 만족해야 한다.

1. 제 3정규형을 만족해야 한다.
2. 모든 결정자가 후보키 집합에 속해야 한다.

<br/> 

#### 예시

<img style="margin-top:0" src="https://velog.velcdn.com/images/wisdom-one/post/668e8b1d-ab8e-4529-9d55-1bf9537ea3c0/image.png"/>

위의 테이블은 (학생번호, 과목)이 기본키로 지도교수를 알 수 있다. 

그러나 지도교수를 알면 과목을 알 수 있으므로, 지도교수 → 과목 이 종속적이다.  

즉, 후보키 집합에 속하지 않은 결정자가 존재하므로 BCNF를 만족하지 않는다.

<br/> 

BCNF를 만족하기 위해서는 다음과 같이 분리하면 된다.

<img style="margin-top:0" src="https://velog.velcdn.com/images/wisdom-one/post/2c54e3d9-a815-4cc8-9f23-68aadbdf9b2c/image.png"/>


<br/>

### 5) 제 4정규화 (4NF)

**" `다치 종속`을 제거한다. "**

4NF는 다음을 만족해야 한다.

1. BCNF를 만족해야 한다.
2. 다중값 종속(다치 종속)이 없어야 한다.

> #### 💡 다치 종속 (Multi-valued Dependency)
> 같은 테이블 내의 독립적인 두 개 이상의 컬럼이 또 다른 컬럼에 종속되는 것을 말한다.  
> 
> 즉, A → B 인 의존성에서 단일 값 A와 다중 값 B가 존재한다면 다치 종속이라고 할 수 있다.  
> 
> 이러한 종속을 A ↠ B 로 표기한다. (다치 종속은 이중 화살표(double arrow) ↠ 로 표기한다.)  
>
> 다치 종속은 최소 2개의 컬럼이 다른 컬럼에 종속되어야 하기 때문에 최소 3개의 컬럼이 필요하다.  
>

<br/> 

#### 예시

![](https://velog.velcdn.com/images/wisdom-one/post/430da4e4-51fb-4e0e-b31a-4602c094eb74/image.png)


위의 테이블은 `Person ↠ Mobile` 과 `Person ↠ Food_Likes` 두 가지 의존성을 가지므로 다치 종속이 존재한다.

<br/>

제 4정규화를 통해 다음과 같이 분리할 수 있다.

![](https://velog.velcdn.com/images/wisdom-one/post/0215ea08-f2d5-4ecc-ab87-94a27475b384/image.png)


<br/>

### 6) 제 5정규화 (5NF)

**" `조인 종속`을 제거한다. "**


5NF는 다음을 만족해야 한다.

1. 4NF를 만족해야 한다.
2. 더 이상 비손실 분해를 할 수 없어야 한다. 

> #### 💡 조인 종속 (Joint dependency)
> 하나의 릴레이션을 여러개의 릴레이션으로 분해하였다가, 다시 조인했을 때 데이터 손실이 없고 필요없는 데이터가 생기는 것을 말한다.    
> 
> 조인 종속성은 다치 종속의 개념을 더 일반화한 것이다.

<br/> 

#### 예제

위의 4NF 테이블에 대해 조인 연산을 수행하면 다음과 같은 결과가 나온다.  

![](https://velog.velcdn.com/images/wisdom-one/post/fee15ae1-3e08-4fa4-905a-d93707e972fe/image.png)

위의 결과를 보면 제 4정규화를 수행하기 전 데이터와 다른 것을 알 수 있다.  

데이터 손실은 없지만 필요없는 데이터가 추가적으로 생겼으므로 5NF를 만족하지 않는다.  

<br/> 

제 5정규화를 통해 다음과 같이 분리할 수 있다.

![](https://velog.velcdn.com/images/wisdom-one/post/8a7c4fd8-b140-4144-b2c2-72cd2cf85955/image.png)


<br/><br/>

## 🔖 참고
- https://bazingzinga.blogspot.com/2019/02/10.html
- https://code-lab1.tistory.com/48
- https://www.geeksforgeeks.org/difference-between-4nf-and-5nf/
