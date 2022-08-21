# 1. 정규화, Normalization

> 관계형 DB의 설계에서 중복을 최소화하여 데이터를 구조화하는 프로세스<br/>
정규화의 목표는 관련이 없는 함수 종속성은 별개의 relation으로 표현하는 것<br/>
정규화의 장점은 이상현상을 발생 가능성을 줄이지만 단점으로는 연산 시간이 증가함<br/>
정규화된 결과를 정규형이라고 하며 정규형은 기본, 고급 정규형으로 나뉨<br/>
> 

- 기본 정규형 : 제1정규형, 제2정규형, 제3정규형, BCNF
- 고급 정규형 : 제4정규형, 제5정규형

<br/>

**keyword**

- 완전 함수 종속 : 어떤 속성이 기본 키에 대해 완전히 종속일 때
- 부분 함수 종속 : 어떤 속성이 기본 키가 아닌 다른 속성에 종속되거나 기본 키가 여러 속성으로 구성되어 있을 경우 기본키를 구성하는 속성 중 일부만 종속될 때

<br/><br/>

# 2. 제1정규형, 1NF

> 릴레이션에 속한 모든 속성의 도메인이 더 이상 분해되지 않는 원자값(Atomic Value)으로만 구성된 정규형
> 

<br/>

**BEFORE**

![image](https://user-images.githubusercontent.com/100047095/185778790-bddbdd96-5ee4-4d16-8672-9f9a2a2e772c.png)
출처 : [https://rebro.kr/160](https://rebro.kr/160)

<br/>

**AFTER**

![image](https://user-images.githubusercontent.com/100047095/185778796-83d77fd3-ebbf-4bfa-8359-59e97cc56b55.png)

<br/>

**이상 현상**

- 삽입 이상 : 학생이 새 과목을 수강신청 할 때 불필요한 정보까지 모두 알아야 함
- 삭제 이상 : 300번 학생이 C400을 취소하면 해당 과목에 대한 정보가 모두 사라짐
- 갱신 이상 : 100번 학생이 지도 교수를 변경하려고 한다면 100번 학생의 모든 정보를 다 바꿔주어야 함

→ 원인 : 기본키가 아닌 속성들이 기본키에 완전 함수 종속되지 못하고 부분 함수 종속되어 있기 때문임, 즉 기본키의 일부 속성에만 의존하고 있기 때문 (아래 그림에서 노란색이 Primary Key)

![image](https://user-images.githubusercontent.com/100047095/185778803-ef4879ea-225a-42ff-a8c4-313b13303778.png)

<br/><br/>

# 3. 제2정규형, 2NF

> 제1정규형이면서 기본키에 속하지 않은 속성 모두가 기본키에 완전 함수 종속인 정규형<br/>
제1정규형에 속하는 릴레이션이 제2정규형을 만족하게 하기 위해서는 부분 함수 종속을 제거하고 모든 속성이 기본키에 완전 함수 종속 되도록 릴레이션을 **분해**하는 과정을 거쳐야 함
> 

![image](https://user-images.githubusercontent.com/100047095/185778809-90e25631-ec76-4d80-a396-369a2dc9707f.png)

<br/>

**BEFORE**

![image](https://user-images.githubusercontent.com/100047095/185778817-2f4dd5c7-c47b-4cc2-ac46-8567eb6048b5.png)

<br/>

**AFTER**

![image](https://user-images.githubusercontent.com/100047095/185778826-f3eaf0d7-89e5-4fb4-b7fd-fa407f97ae0c.png)

<br/>

**이상 현상**

1. 삽입 이상 : 지도교수가 학과에 소속되어 있음을 나타내기 위해 무조건 지도 학생이 있어야 함
2. 삭제 이상 : 300번 학생이 자퇴하는 경우 교수 P3의 정보가 사라짐
3. 갱신 이상 : 지도교수의 학과가 변경되는 경우 모두 찾아서 변경해주어야 함 

→ 원인 : 이행적 함수 종속성 (Functional Dependency) 을 가지고 있기 때문, 이는 A→B B→C A→C의 관계를 가진 것을 말함

<br/><br/>

# 4. 제3정규형, 3NF

> 제2정규형이면서 Functional Dependency를 모두 제거한 정규형<br/>
→ 기본키에 속하지 않은 모든 속성이 기본키에 Functional Dependency 관계가 아닐 때
> 

![image](https://user-images.githubusercontent.com/100047095/185778830-bad26564-8259-4e09-aab7-6faff8e1438c.png)

<br/>

**BEFORE**

![image](https://user-images.githubusercontent.com/100047095/185778835-0d4958f1-a147-4dd5-a996-66cd1351b35b.png)

<br/>

**AFTER**

![image](https://user-images.githubusercontent.com/100047095/185778839-cec7b79d-10d0-498f-9695-e1516a1b81aa.png)

<br/><br/>

# 5. BCNF

> Boyce and Codd Normal Form <br/>
제3정규형을 강화시킨 개념으로 모든 결정자가 항상 후보키가 되도록 릴레이션을 분해한 것
> 

![image](https://user-images.githubusercontent.com/100047095/185778845-ccc13e7b-52fb-4312-8ccc-e4df7a05defa.png)

상단의 테이블에서는 Functional Dependency를 만족하지 않아 제3정규형을 만족하지만 이상현상은 존재함

- 삽입 이상 : 새로운 교수가 특정 과목을 담당한다면 수강생이 없을 때는 추가하지 못함
- 삭제 이상 : 학번 100인 학생이 C234 과목을 수강 취소한다면 P2가 담당한다는 정보도 사라짐
- 갱신 이상 : P1이 담당한 C123이 P3가 담당하게 된다면 모든 항목을 찾아 변경해주어야 함

→ 원인 : 결정자(Determinant)가 후보키(Alternative Key)로 취급되고 있지 않기 때문

후보키는 SuperKey 중 최소성을 갖는 키이므로 이 테이블에서는 (학번, 과목명), (학번, 담당교수)가 후보키가 됨. 그러나 담당 교수 만으로는 유일성을 만족하지 못하므로 후보키가 될 수 없음

하지만 후보키가 아님에도 담당 교수는 과목명을 결정할 수 있기에 결정자임 

→ 따라서 Determinant인 담당 교수가 후보키가 되도록 분해해주면 BCNF를 만족하게 됨

![image](https://user-images.githubusercontent.com/100047095/185778854-4bbea783-45cf-4012-80d8-83febea15bb4.png)

