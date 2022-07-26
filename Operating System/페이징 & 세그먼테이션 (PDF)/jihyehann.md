# 💡 페이징과 세그먼테이션
## 1. 메모리 관리

다중 프로그래밍 시스템에 여러 프로세스를 수용하기 위해 주 기억 장치(RAM)를 동적 분할하는 메모리 관리 작업이 필요하다. 하드디스크에 있는 프로그램을 메인 메모리에 어떻게(연속적 or 불연속적) 적재할 것인지 판단해야 한다.


### 1) 연속 메모리 관리

프로그램 전체가 하나의 커다란 공간에 연속적으로 할당되어야 한다.

- 고정 분할 기법 : 주기억장치가 고정된 파티션으로 분할된다. (내부 단편화 발생)
- 동적 분할 기법 : 파티션들이 동적 생성되며 자신의 크기와 같은 파티션에 적재한다. (외부 단편화 발생)

### 2) 불연속 메모리 관리

프로그램의 일부가 서로 다른 주소 공간에 할당될 수 있는 기법이다.

- 페이징 (Paging) : 프로세스를 고정 크기로 분할
- 세그멘테이션 (Segmentation) : 프로세스를 서로 다른 크기의 논리적 단위로 분할

<br/>

## 2. 단편화 (Fragmentation)

단편화(Fragmentation)란, 기억 장치의 빈 공간 또는 자료가 여러 조각으로 나뉘는 현상이다.

이러한 단편화는 2가지로 나뉜다.

### 1) 내부 단편화 (Internal Fragmentation)

<img width="50%" 
     src="https://user-images.githubusercontent.com/75151848/194740509-2ee73b1a-0437-4441-b126-ce939e62d878.png"/>

- 프로세스가 사용하는 메모리 공간에 남는 부분. 
- 프로세스가 요청한 양보다 더 많은 메모리를 할당할 때 발생한다.

### 2) 외부 단편화 (External Fragmentation)

<img width="50%" 
     src="https://user-images.githubusercontent.com/75151848/194740515-ded24ad9-cd58-4a98-a129-e6035b157a17.png"/>

- 메모리 공간 중 사용하지 못하게 되는 부분.
- 메모리 할당 및 해제 작업의 반복으로 작은 메모리가 중간 중간 존재하여, 총 메모리 공간은 충분하지만 실제로 할당할 수 없는 상황이다.

<br/>

## 3. 가상 메모리 (Virtual Memory)

메모리가 실제 메모리보다 많아 보이게 하는 기술로, 프로세스 전체를 메모리에 올리지 않고 작은 조각으로 나누어 그 중 일부분만을 메모리에 비연속적으로 적재하는 것을 말한다. 

가상 메모리를 위해서는, 먼저 모든 프로그램을 조각들로 나눠야 한다.  
이때 조각들의 크기를 모두 같도록 하면 한 조각을 `페이지(Page)` 라고 부르고, 서로 다르게 하면 한 조각을 `세그먼트(Segment)` 라고 부른다. 

`페이지` 와 `세그먼트` 가 메모리와 디스크 사이의 전송 단위가 되며, 이것을 일반적으로 블록(Block)이라고 부른다.

<br/>

## 4. 페이징 (Paging)

프로세스를 **일정한 크기**의 페이지로 분할해서 메모리에 적재하는 방식이다.

- 페이지 : 고정 사이즈의 가상 메모리 내 프로세스 조각
- 프레임 : 페이지 크기와 같은 주 기억 장치의 메모리 조각

물리 메모리는 페이지와 같은 크기의 `프레임` 으로 나눠지며, 페이지와 프레임에는 일련의 번호가 매개진다.

<br/>

### 주소 변환 

<img width="70%" 
     src="https://user-images.githubusercontent.com/75151848/194741683-74a90b75-d9ca-4023-bcd8-6c7dbd53d62a.png"/>

운영체제는 가상주소를 실주소로 변환하기 위해 프로세스당 하나의 페이지 테이블(Page Mapping Table, PMT) 을 만들어 두어야 하며, 이 테이블의 크기는 해당 프로세스의 페이지 개수에 비례한다. 

페이지 테이블에는 `프레임 번호` 가 저장되어 있다.

논리 주소 (Logical Address)는 `<page, offset>` 과 같은 형태로 구성되며, 물리 주소로 변환하면 `<frame 번호, offset>` 형태가 된다.


### 특징
- 논리 메모리는 물리 메모리에 저장될 때 연속되어 저장될 필요가 없고, 물리 메모리의 남는 프레임에 적절히 배치되기 때문에 외부 단편화가 생기지 않는다.
- 내부 단편화 문제가 발생할 수 있다. 페이지 단위를 작게하면 해결할 수 있지만, 페이지 매핑 과정이 복잡해져 오히려 비효율적이다.

<br/>

## 5. 세그멘테이션 (Segmentation)

프로세스를 물리적 단위인 페이지가 아닌 **논리적 단위**인 세그먼트로 분할해서 메모리에 적재하는 방식이다.

- 세그먼트 (segment) : 가상 메모리를 서로 크기가 다른 논리적 단위로 분할한 것

### 주소 변환

<img width="70%"
     src="https://user-images.githubusercontent.com/75151848/194741623-6e82254e-705e-438c-a913-79bd7da7f98c.png"/>

세그먼트 테이블에는 `시작주소(base)` 와 `세그먼트 크기(limit)` 가 저장되어 있다.

논리 주소는 `<segment, offset>` 형태로 구성되며, 물리 주소로 변환하면 `<base, offset>` 형태가 된다.


### 특징

- 내부 단편화 문제가 해소된다.
- 외부 단편화 문제가 생길 수 있다.

<br/><br/>

## 🔖 참고
- [[운영체제] 페이징과 세그멘테이션](https://steady-coding.tistory.com/524)
- https://dar0m.tistory.com/269
