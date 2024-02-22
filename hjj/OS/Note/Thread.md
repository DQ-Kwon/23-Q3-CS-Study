# Thread <sub>스레드</sub>

## :bookmark_tabs: 목차

[:arrow_up: **OS**](../README.md)

1. ### Thread
   - [:page_facing_up: thread](#cors-cross-origin-resource-sharing-1)
   - [:page_facing_up: PCB](#pcb-process-control-block-프로세스-제어-블록)
   - [:page_facing_up: context switching](#context-switching-문맥-교환)
   - [:page_facing_up: 프로세스 스케줄링](#context-switching-문맥-교환)
   - [:page_facing_up: 프로세스간 통신](#context-switching-문맥-교환)
   - [:page_facing_up: IPC](#context-switching-문맥-교환)


## Thread <sub>스레드</sub>

> 한 프로세스 내에서 나뉘어진 하나 이상의 실행 단위

- 프로세스 내부에는 최소 하나의 스레드 <sub>thread</sub>를 가지고 있음.
- 스레드 : 프로세스 내의 실행 흐름 단위
- 프로세스끼리는 기본적으로 자원공유하지 않음.
- 프로세스 내 스레드끼리는 같은 프로세스 내의 자원을 공유함.

## PCB <sub>Process Control Block, 프로세스 제어 블록</sub>

- 프로세스를 식별하기 위한 정보를 저장하는 자료 구조
- <u>커널 영역</u>에 생성됨.
- **PCB 생성** : 프로세스 생성 시
    - '새로운 프로세스가 생성되었다.' == '운영체제가 PCB를 생성했다.'
- **PCB 폐기** : 프로세스 실행 종료 시
    - '프로스세가 종료되었다.' == '운영체제가 해당 PCB를 폐기했다.'
- PCB에 담기는 정보
    - 아래 정보들을 [문맥](#context-switching-문맥-교환)이라고 할 수 있음.
    - `PID` <sub>Process ID, 프로세스 ID</sub>
        - 특정 프로세스를 식별하기 위해 부여하는 고유 번호
    - `레지스터 값`
        - 레지스터: CPU 내부의 작은 임시 저장 장치로 프로그램을 실행하는 데 필요한 값들을 임시로 저장함.
        - 프로세스는 자신의 차례가 돌아오면 이전에 실행하며 사용했던 레지스터의 중간값들을 모두 복원함.
    - `프로세스 상태`
        - 현재 프로세스가 어떤 상태인지 기록해야 함.(입출력 장치 사용을 기다리고 있는지, CPU를 사용하기 위해 기다리고 있는지, CPU를 이용하고 있는 상태인지 등)
    - `CPU 스케줄링 정보`
        - 프로세스가 언제, 어떤 순서로 CPU를 할당받을지에 대한 정보도 PCB에 기록함.
    - `메모리 관리 정보`
        - 프로세스가 어느 주소에 저장되어 있는지, 페이지 테이블 정보가 담겨 있음. 
        - 왜냐하면 프로세스마다 메모리에 저장된 위치가 다르기 때문에 주소를 저장해야 함.
    - `사용한 파일과 입출력장치 목록`
        - 어떤 입출력장치가 이 프로세스에 할당되었는지, 어떤 파일들을 열었는지에 대한 정보들이 기록됨.

</br>

## context switching <sub>문맥 교환</sub>

- 문맥 <sub>context</sub>
    - 하나의 프로세스 수행을 재개하기 위해 기억해야 할 정보
    - 하나의 프로세스 문맥은 해당 프로세스의 PCB에 표현되어 있음.


</br>

---

- 참고

    혼자 공부하는 컴퓨터 구조 + 운영체제

    [[운영체제] 프로세스란? (스케줄링, 메모리구조, 상태변화)](https://blockdmask.tistory.com/22)

    []()

    []()
    
    []()