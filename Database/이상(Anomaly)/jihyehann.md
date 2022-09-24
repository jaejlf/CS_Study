# 💡 이상(Anomaly)

## 1. 개념

릴레이션 조작 시 데이터들이 불필요하게 중복되어 예기치 않게 발생하는 현상을 말한다. 

좋은 관계형 데이터베이스를 설계하는 목적 중 하나가 이상 현상이 생기지 않도록 고려해 설계하는 것이다.

`정규화`를 통해 이상 현상을 방지할 수 있다.

이상 현상의 종류에는 `삽입 이상`, `갱신 이상`, `삭제 이상`이 있다.

- 삽입 이상 (Insertion Anomaly) : 불필요한 정보를 함께 저장하지 않고서는 어떤 정보를 저장하는 것이 불가능한 상황.
- 갱신 이상 (Update Anomaly) : 반복된 데이터 중에 일부를 갱신할 때 데이터의 불일치가 발생하는 상황.
- 삭제 이상 (Deletion Anomaly) : 필요한 정보를 함께 삭제하지 않고서는 어떤 정보를 삭제하는 것이 불가능한 상황.

<br/>

## 2. 예시

<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-style="style8" data-ke-align="alignLeft">
 <tbody>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학번</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학생명</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과 코드</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과명</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과장 코드</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과장명</b></td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">1</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">도우너</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">101</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">경영학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">1000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">워런 버핏</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">2</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">고길동</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">101</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">경영학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">1000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">워런 버핏</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">3</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">또치</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">102</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">물리학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">2000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">아인슈타인</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">4</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">마이콜</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">102</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">물리학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">2000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">아인슈타인</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">5</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">둘리</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">103</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">컴퓨터공학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">3000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">빌 게이츠</td>
  </tr>
 </tbody>
</table>
 
<br/>
 
### 1) 삽입 이상 (Insertion Anomaly)

<img width="60%" 
     src="https://user-images.githubusercontent.com/75151848/192076497-8153025a-f599-4605-81a2-927ad2af7460.png"/>

신설 학과 '수학과'에 아직 학생이 존재하지 않는다고 가정하자. 

이때 대학교 학생이 존재하지 않기 때문에 테이블에 데이터를 추가할 수 없다. 

<br/>

### 2) 갱신 이상 (Update Anomaly)

<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-style="style8" data-ke-align="alignLeft">
 <tbody>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학번</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학생명</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과 코드</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과명</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과장 코드</b></td>
   <td style="width: 16.6667%; height: 20px; text-align: center;"><b>학과장명</b></td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">1</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">도우너</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">101</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">경영학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">1000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">워런 버핏</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">2</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">고길동</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">101</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">경영학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">1000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">워런 버핏</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">...</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">...</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">...</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">...</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">...</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">...</td>
  </tr>
  <tr style="height: 20px;">
   <td style="width: 16.6667%; height: 20px; text-align: center;">100</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">둘리</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">101</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">경영학과</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">1000</td>
   <td style="width: 16.6667%; height: 20px; text-align: center;">워런 버핏</td>
  </tr>
 </tbody>
</table>

경영학과의 학과장이 이름을 개명해서 학과장명을 변경해야 하는 경우를 생각해보자.

이때 경영학과 학생의 수만큼 데이터를 변경하지 않으면, 데이터 불일치가 발생한다.

즉, 학생이 100명이라면 100개의 데이터를 변경해야 한다.

<br/>

### 3) 삭제 이상 (Deletion Anomaly)

<img width="60%" 
     src="https://user-images.githubusercontent.com/75151848/192076767-fd5eaca3-4b3e-4648-a2f8-1de720bb344c.png"/>


컴퓨터공학과의 학생이 둘리 1명일 때, 둘리 학생이 자퇴를 하여 데이터를 삭제해야 하는 경우를 생각해보자.

이때 둘리의 데이터를 삭제하면 컴퓨터공학과에 대한 정보도 사라지게 된다.

<br/><br/>

> ### 🔖 참고
> - https://wkdtjsgur100.github.io/anomaly/
> - https://developer-talk.tistory.com/256
