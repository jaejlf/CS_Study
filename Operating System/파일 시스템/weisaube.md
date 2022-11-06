# 파일 시스템

## 📌 A. 파일과 파일 시스템

<br/>

- 파일: 논리적인 저장 단위로, 관련된 정보 자료들의 집합에 이름을 붙인 것이다. 컴퓨터 시스템의 편리한 사용을 위해 정보 저장의 일괄된 논리적 관점을 제공
  - 레코드(Record) 혹은 블록(Block) 단위로 비휘발성 보조기억장치에 저장
- 파일 속성(File attribute) 또는 파일의 메타데이터(metadata): 파일을 관리하기 위한 각종 정보
- 파일 시스템(File System): 운영체제와 모든 데이터, 프로그램의 저장과 접근을 위한 기법을 제공
  - 시스템 내의 모든 파일에 관한 정보를 제공하는 계층적 디렉터리 구조
  - 파일 및 파일의 메타데이터, 디렉터리 정보 등 관리

<br/>

## 📌 B. 접근 방식

<br/>

시스템이 제공하는 파일 정보의 접근 방식으로는 순차 접근(Sequential Access)과 직접 접근(Direct Access, Random Access), 색인 접근(Index Access)으로 나뉜다.

<br/>

### 1. 순차 접근(Sequential Access)

- 가장 단순한 방법
- 파일의 정보가 레코드 순서대로 처리
- 현재 위치에서 읽거나 쓰면 offset이 자동으로 증가하고, 뒤로 돌아가기 위해서는 되감기 필요

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn9ifN%2Fbtrgvqo8ivJ%2F5nWEa4e9rKUK9MBtPRqyCK%2Fimg.png" alt="text" width="485" />
</p>

<br/>

### 2. 직접 접근(Random Access)

- 파일의 레코드를 임의의 순서로 접근 가능
- 읽기나 쓰기의 순서에 제약이 없으며, 현재 위치를 유지할 수 있다면 이를 통해 순차 접근 기능도 구현 가능

<br/>

### 3. 색인 접근(Index Access)

- 파일에서 레코드를 찾기 위해 색인을 먼저 찾고 대응되는 포인터 얻음
- 이를 통해 파일에 직접 접근하여 원하는 데이터를 얻을 수 있음
- 크기가 큰 파일에 유용

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FucSgw%2Fbtrgqyn2f1Z%2FrTRsabKKW7LPca4o5307L0%2Fimg.png" alt="text" width="485" />
</p>

<br/>

## 📌 C. 디렉터리 구조

- 디렉터리(Directory): 파일의 메타데이터 중 일부를 보관하고 있는 일종의 특별한 파일
  - 해당 디렉터리에 속한 파일의 이름과 속성 포함

디렉터리의 논리적 구조는 다음과 같다

<br/>

### 1단계 디렉터리(Single-Level Directory)

- 모든 파일들이 디렉터리 밑에 존재하는 형태
- 파일들은 서로 유일한 이름을 가지고 서로 다른 사용자라도 같은 이름을 사용할 수 없음
- 지원하기도 쉽고 이해하기도 쉽지만, 파일이 많아지거나 다수의 사용자가 사용하는 시스템에서는 심각한 제약을 가짐

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbbk9x6%2FbtrgpwxekSY%2FLC5Y2BhsAypMTbdWfMToRK%2Fimg.png" alt="text" width="485" />
</p>

<br/>

### 2단계 디렉터리(Two-Level Directory)

- 각 사용자 별로 별도의 디렉터리를 갖는 형태

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlLfBK%2FbtrgxCCjMG6%2FeRQ02qksvFI7JIGQZ2KZdK%2Fimg.png" alt="text" width="485" />
</p>

<br/>

- UFD: 자신만의 사용자 파일 디렉터리
- MFD: 사용자의 이름과 계정 번호로 색인되어 있는 디렉터리. 각 엔트리는 사용자의 UFD를 가리킴

서로 다른 사용자가 같은 이름의 파일을 가질 수 있고 효율적인 탐색이 가능.
하지만 그룹화가 불가능하고, 다른 사용자의 파일에 접근해야 하는 경우에는 단점이 된다.

<br/>

### 트리 구조 디렉터리(Tree-Structured Directory)

- 사용자들이 자신의 서브 디렉터리(Sub-Directory)를 만들어서 파일을 구성
- 하나의 루트 디렉터리를 가지며 모든 파일은 고유한 경로(절대 경로/상대 경로)를 가짐
  - 효율적인 탐색이 가능하고, 그룹화가 가능
- bit를 사용하여 0이면 일반 파일, 1이면 디렉터리로 구분

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fk8pMk%2Fbtrgx0JQ4zK%2FZw5OniN9knvCQxKTDBJ3P1%2Fimg.png" alt="text" width="485" />
</p>

<br/>

### 4. 비순환 그래프 디렉터리(Acyclic-Graph Directory)

<br/>

- 디렉터리들이 서브 디렉터리들과 파일을 공유할 수 있도록 한다
  - 트리 구조의 디렉터리를 일반화한 것
- 참조되는 파일에 참조 계수를 두어서, 참조 계수가 0이 되면 파일을 참조하는 링크가 존재하지 않는다는 의미이므로 그때 파일을 삭제할 수 있도록 한다

<br/>

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc1f9RF%2FbtrgvUpXqh3%2FIDPjd6TkDgHQYuURltRmKk%2Fimg.png" alt="text" width="485" />
</p>

<br/>

## 📌 D. 참고 자료

🔗 [[운영체제(OS)] 11. 파일 시스템(File System)](https://rebro.kr/181)
