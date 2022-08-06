# 1. 프로세스 주소 공간?

> 프로세스는 운영체제가 자원을 할당하는 단위 <br/>
→ 프로세스가 운영체제로부터 메모리를 할당 받는데 이를 **프로세스 주소 공간**이라고 함 <br/>
프로세스 주소 공간은 Code Segment, Data Segment, Stack Segment로 나뉘어짐 <br/>
(그 외에도 Heap Segment, BSS가 있음) <br/>
> 

![image](https://user-images.githubusercontent.com/100047095/183112118-e3aaa875-6f7b-4ba2-a49a-1ae019878589.png)

출처 : [https://whereisusb.tistory.com/10](https://whereisusb.tistory.com/10)

<br/>

### a. Code Segment, 코드

- 프로그램의 코드가 저장되어 있는 부분
- 읽기만 가능
- 프로그램의 코드는 프로그램이 만들어지고 나서는 바뀔 일이 전혀 없음, 따라서 Read-Only임 그렇기에 같은 프로그램을 실행시켜 몇 개의 프로세스가 실행되더라도 코드 부분은 다 똑같은 내용을 가지고 있게 됨 → 메모리 사용량을 줄이기 위해 같은 프로그램의 프로세스일 경우 코드 부분을 공유함

<br/>

### b. Data Segment, 데이터

- 전역 변수, Static 변수 같은 데이터가 저장되어 있는 부분
- 읽고 쓰기가 가능
- 프로그램의 시작과 함께 할당되며 프로그램이 종료 되면 소멸함

<br/>

### c. Stack Segment, 스택

- 함수(function)나 지역 변수(local variables)가 저장되어 있는 부분
- 읽고 쓰기가 가능
- 메모리의 높은 주소에서 낮은 주소의 방향으로 할당됨
    - 프로그램이 실행되며 메모리를 얼마나 사용할지 미리 계산 X
    따라서 Stack 함수의 뒷부분부터 변수의 주소가 매겨짐
- 컴파일 타임에 크기가 결정되기 때문에 무한히 할당할 수 없음 → 그래서 재귀 함수가 너무 깊게 호출되거나 함수가 지역 변수를 너무 많이 가지고 있어 stack 영역을 초과하면 stack overflow가 발생

<br/>

### d. Heap Segment, 힙

- 참조형의 데이터 값이 저장됨
- 런타임에 크기가 결정되는 메모리 영역
- Heap은 메모리의 낮은 주소에서 높은 주소의 방향으로 할당 됨
- Heap과 Stack은 사실상 같은 주소를 공유함
Heap이 메모리 위쪽 주소부터 할당되면 Stack은 아래부터 할당
따라서 각 영역이 상대 공간을 침범할 수 있는데 이를 각각 Heap, Stack Overflow라고 함 
(하지만 stack overflow는 위에 서술한 바와 같이 정해진 Stack 영역을 초과해서 발생하는 경우가 왕왕 많음)

<br/>

### e. BSS, Block Stated Symbol

- 초기값 없는 전역변수, 배열, static 변수가 저장되어 있는 부분
- 초기화 된 데이터는 Data 영역, 초기화 되지 않은 데이터는 BSS에 저장됨
    - 초기화 되지 않은 변수는 프로그램이 실행될 때 영역만 잡아주면 되고 그 값을 프로그램에 저장하고 있을 필요가 없으나 초기화 되는 변수는 그 값도 프로그램에 저장하고 있어야하므로 BSS가 아닌 Data 영역에 저장 됨.

<br/><br/>

# 2. Compile Time vs Run Time

> **Compile Time** : 소스코드를 작성하고 컴파일이라는 과정을 통해 기계어 코드로 변환되어 실행 가능한 프로그램이 되는데 이때를 컴파일 타임이라고 함<br/>
**Run Time** : 프로그램이 사용자에 의해 실행되어지며 이때를 런타임이라고 함<br/>


<br/>

| Compile Time | Run Time |
| --- | --- |
| Code | Stack |
| Data | Heap |
| BSS |  |
| 크기 고정 O | 크기 고정 X |

<br/><br/>

# 3. Stack, Data 부분 분리?

<br/>

### a. 역할 분배를 위함

Stack은 LIFO의 구조임 

→ Stack을 이용해 함수의 흐름을 관리하고 Data 영역을 이용해 전역변수, 정적(static) 변수를 관리함 

아래 그림에서의 함수의 예시를 보면 함수와 지역변수의 경우 Stack에 저장해서 사용하면 되지만 전역변수의 경우에는 어떤 함수에서도 접근할 수 있어야 하므로 Data 부분에 저장 

![image](https://user-images.githubusercontent.com/100047095/183112202-49fd13ae-0214-4704-bb21-b87eb5e75564.png)

![image](https://user-images.githubusercontent.com/100047095/183112212-851109e6-9dc5-4177-96e2-95bae8680cf9.png)

출처 : [https://whereisusb.tistory.com/10](https://whereisusb.tistory.com/10)

<br/>

### b. 스레드의 경우 Data 영역의 공유

스레드는 각각 stack만 다르고 code, data, heap은 공유해서 사용한다고 했었음

이와 같이 Data를 따로 구분지어 놓으면 각각의 스레드가 Data 영역을 공유하므로 똑같은 공간을 여러개 만들지 않아도 됨

그러나 Data 영역을 공유하기 때문에 동기화 이슈가 발생… 

✅ 메모리 절약 가능
