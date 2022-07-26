# 📍 프로세스 주소 공간

![image](https://user-images.githubusercontent.com/78673570/183587948-fc3b818d-b12d-433a-ba32-7a0e334e3d44.png)

프로세스가 메모리를 할당받으면, 자신만의 방법으로 이 공간을 `프로세스 주소 공간`의 구조로 관리한다.

<br>

## Text (Code 영역)

- 실행 가능한 명령어가 포함된 오브젝트 파일 또는 메모리 공간을 할당받은 프로그램 섹션 중의 하나
- 프로그램이 텍스트 영역의 명령어를 변경하지 못하도록 읽기 전용(Read-Only)인 경우가 많다.
- 힙/스택에 의해 메모리 공간이 덮어씌워지지 않도록, 일반적으로 힙/스택 메모리 공간 아래에 위치한다.
- 프로세스가 종료될 때까지 유지되는 영역

<br>

## Data 영역

- "초기화 된" 데이터 영역
- 프로그램의 가상 주소 공간의 일부분으로써, 초기화된 전역 변수와 static 변수를 포함한다.
- 프로그램의 시작과 함께 할당되며, 프로그램이 종료되면 소멸한다.

<br>

## BSS 영역

= Block Started by Symbol

- "초기화 되지 않은" 데이터 영역
- 프로그램의 실행과 함께 커널에 의해 0으로 초기화된다.

<br>

## Heap 영역

- 개발자에 의한 동적 메모리 할당이 수행되는 영역
- malloc으로 동적 할당이 된 변수
- 메모리의 낮은 주소 → 높은 주소의 방향으로 할당된다.

<br>

## Stack 영역

- LIFO 구조를 가지는 프로그램 스택으로, 일반적으로 메모리 상위 주소에 위치한다.
- 새로 호출된 함수는 스택 메모리 공간에 지역 변수를 위한 공간을 할당하고, 데이터와 함께 지역 변수를 저장한다.
- 함수가 호출될 때마다 새로운 스택 프레임이 생성된다.
- 메모리의 높은 주소 → 낮은 주소의 방향으로 할당된다.
- 재귀 함수가 너무 깊게 호출되거나, 함수가 지역 변수를 너무 많이 가지고 있어 스택 영역을 초과하면 `stack overflow` 에러가 발생한다.

<br>

## cf. 영역의 분리

- Data 영역과 BSS 영역의 분리
- Stack 영역과 Data 영역의 분리 : 한 프로세스가 여러개의 스레드를 가질 때, 각각의 스레드는 자신만의 Stack 영역을 가진다.
반면 Data 영역은 공유한다. 즉, 각각의 스레드가 자원을 공유함으로써 메모리를 절약할 수 있다. <br><br> => 메모리 공간을 효율적으로 사용하기 위해
