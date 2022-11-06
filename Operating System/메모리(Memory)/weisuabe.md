# 메모리

## 📌 A. 메인 메모리(주기억장치)

> 데이터와 프로그램을 저장

- 전형적인 휘발성(volatile)이기 때문에 컴퓨터가 셧다운될 경우 메모리의 내용이 없어지게 됨
- CPU가 직접 접근할 수 있는 기억 장치
- 프로세스가 실행되려면 프로그램이 메모리에 올라와야 함.

<br>

CPU는 레지스터가 지시하는대로 메모리에 접근하여 다음에 수행할 명령어를 가져옴

명령어 수행 시 메모리에 필요한 데이터가 없으면 해당 데이터를 우선 가져와야 함

이 역할을 하는 것이 바로 MMU.

<br/>

## 📌 B. MMU(Memory Management Unit, 메모리 관리 장치)

<br/>

- 논리 주소를 물리주소로 변환해 준다.

- 메모리 보호나 캐시 관리 등 CPU가 메모리에 접근하는 것을 총 관리해주는 하드웨어

<br/>

<p align="center">
  <img src="https://velog.velcdn.com/images%2Fayoung0073%2Fpost%2F42fdbecb-1d9c-4693-b382-0aa05f956056%2Fimage.png" alt="text" width="485" />
</p>

1. CPU가 Logical Address 346을 요청
2. MMU가 안에 있는 14,000을 더하여 Physical Memory 14346번지에 있는 내용 참조

<br/>

<br/>

### MMU의 역할

- 가상 주소를 실제 물리 주소로 변환
- 메모리 보호를 위한 메모리 접근 제어
- 운영체제 영역과 사용자 영역을 구분 관리하는 등
- 캐시 메모리 관리
- 버스 중재 등

<br/>

### MMU의 memory protection

<br/>

운영체제의 기능은 크게 CPU 관리, 메모리 관리, I/O 관리가 있다.
메모리 관리를 위해서는 memory protection이 필요하다.

- memory protection: 잘못된 메모리 번지를 참조하지 않도록 막아줌

<br/>

- 프로그램의 주소공간이 물리적 메모리에 연속적으로 적재되는 것으로 가정
- 프로세스가 CPU를 얻을때마다 Base Register 값과 Limit Register 값을 재설정
- 물리적 주소값 = 논리적 주소값 + Base register(=reloaction register) 값
- 논리적 주소값이 OffSet 역할
- Limit register은 메모리보안(memory protection) 역할을 수행(논리적 주소값이 한계레지스터 값보다 작은지 체크, 그렇지 않다면 트랩발생 후 프로세스 강제종료)

<br/>

## 📌 C. 참고 자료

🔗 [운영체제(OS) - 6. 메모리 관리](https://developer-ping9.tistory.com/43)

🔗 [[운영체제 OS] MMU(Memory management unit)란? contiguous allocation(연속메모리 할당) MMU와 메모리분할 문제, 메모리관리장치](https://jhnyang.tistory.com/247)
