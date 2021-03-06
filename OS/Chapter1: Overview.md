# OS

## 🔨 컴퓨터 시스템 요소

- 하드웨어(CPU, 메모리, 입출력 장치)
- 운영체제
- 어플리케이션 프로그램
- User

## 1. OS가 하는 일

- 하드웨어 관리
- 하드웨어, 소프트웨어, 유저를 매개
- 커널과 커널 모듈로 구성
    - 커널이 핵심!
    - 커널이 같으면 같은 OS로 취급해요.
1. `os는 정부!`
    - 그 자체 : 무쓸모
    - BUT 사람들에게 좋은 환경 제공! (프로그램들이 유용한 일을 할 수 있도록 환경 제공)
2. User View, System View 두 가지로 나눠볼 수 있어요.

### 😀 User View

- 사용자가 컴퓨터 쉽게 사용할 수 있도록 컴퓨터 리소스를 분배해요.
- 여러명 일 경우 공평하게

### 😀 System View

- 시스템에게는 자원 할당자 역할을 합니다.
- CPU time, 메모리 공간, 파일 저장 공간, 입출력 장치 등 다양한 컴퓨터 자원을 위한 제어 프로그램 역할을 합니다.

---

## 2. 컴퓨터 시스템 구조

### 😀 기본 구조

- CPU / Device Controller (디스크, 마우스 키보드, 프린터, ...)
    - 이들은 Common Bus로 이어져 메모리를 공유해요.

### 😀 컴퓨터 부팅

1. 부트스트랩 프로그램 실행 (int ROM,EEPROM) - 펌웨어라고도 해요.
2. `부트스트랩 프로그램` : 시스템 초기화 → 부트 로더 실행 (멀티 부팅 컴퓨터는 부트로더가 여러 OS를 관리하는데 어느 OS를 실행할지 선택합니다.) → OS 실행
3. 커널 로드 → User, System에 서비스 제공 (일부는 커널 외부에서 제공해요. 예를 들면 시스템 프로세스, 시스템 데몬..)

### 😀 컴퓨터 시스템 Operation

- Device Controller 는 인터럽트를 통해 이벤트 발생을 CPU에게 알려요.
- CPU는 이런 이벤트를 받아 우선순위를 기준으로 커널이 작업을 처리할 수 있도록 해줘요.

👉 `인터럽트`

- 하드웨어 : 시스템 버스를 통해서 CPU로
- 소프트웨어 : 시스템 콜을 통해서 CPU로, 특별히 `TRAP`이라고 불러요.

### 😀 **Common Functions of Interrupts**

- 인터럽트를 받은 CPU는 동작을 잠시 멈추고 메모리의 특정 위치를 찾아요. → 이 위치는 인터럽트 벡터에 저장되어 있어요.
- `인터럽트 벡터` : 인터럽트 처리할 수 있는 서비스 루틴들의 주소를 가지고 있어요.

### 😀 인터럽트 Handling

- `폴링(Polling)`
    - 주기적으로 이벤트를 감시하여 처리 루틴 실행
    - 하지만 계속 보니깐 자원을 낭비하게 되겠죠?
- 현대 OS는 대부분 `인터럽트 주도적`
    - 👉 인터럽트 발생 전까지는 CPU가 대기 상태입니다.

---

## 3. I/O Structure

- `입출력 컨트롤러`는 각기 다른 장치를 담당해요.
- 이 컨트롤러들은 각 장치를 위한 `Device Driver`를 가지고 있어요.
- Device Driver → Device Controller의 레지스터를 로드 → Device Controller는 동작을 읽고 로컬 버퍼로 데이터를 전송 → 전송 끝나면 Device Driver에게 인터럽트 보냄 → OS로 통제권을 돌려줌
    
    👉 즉, Device Driver  ↔ Device Controller 상호작용하며 동작을 읽고 해당 동작을 수행할 수 있도록 OS에 입출력을 요청해요.
    

---

## 4. **Direct Memory Access Structure**

- `옛날` : Device Data → CPU → Memory (PIO방식) / CPU 비효율
- `현재`
    - DMA 사용
    - DMA는 메모리 일부에 할당
    - DMA Controller가 DMA 제어
    - 버스를 통해 Device Data ↔ Memory
    - CPU는 전송 완료 인터럽트 한 번이면 끝남

---

## 5. **Computer-System Architecture**

- 현대 컴퓨터 : `폰 노이만 구조`

### 😀 Single-Processor Systems

- 1 컴퓨터 1 메인 CPU
- 장치에 따라 하나의 목적을 가진 프로세서

### 😀 **Multiprocessor Systems**

- 1 컴퓨터 多 프로세서
- 장점이 많아요.
    - 처리량 증가
    - 규모의 경제 (여러 개 싱글 프로세서보다 하나의 멀티가 더 경제적)
    - 신뢰성 증가 : 프로세서 하나가 멈춰도... 버텨!
        - 우아한 성능저하(Graceful degradation)
        - 장애 허용 시스템(Fault tolerant)
- 비대칭 멀티 프로세싱 (Asymmetric) vs 대칭 멀티프로세싱 (Symmetric)
    - 비대칭
        - 보스 프로세서가 전부 제어
        - 부하 분산을 효율적
        - 하지만 보스가 죽으면 부하들도 멈춰요.
    - 대칭
        - 보스 없는 자유로운 회사
        - 한 명이 휴가 나가도 다른 친구들이 일을 분담하고
        - 돌아와서 다시 일을 같이 하는 공유 메모리 문화가 좋아요.

### 😀 **A Dual-Core Design**

- 하지만 CPU 늘린다고 무작정 좋은 건 아니예요.
    - 프로세서 통신 간 비용 증가해요.
    - 사공이 많으면 배가 산으로 가는 느낌!
- `따라서 요즘 트렌드는 좀 다르죠.`
    
    👉 1 Chip 多 Cores 멀티코어
    
    - 칩 외부보다 칩 내부 통신이 빠르기 때문에 더 효율적
    - CPU  → CPU Core 0, 1, 2, 3 .... CPU를 또 쪼갠다는 느낌

### 😀 **Clustered Systems**

- 멀티 프로세서 시스템의 일종이예요.
- 여러 CPU 모아둔 구조입니다.
- `다른 점이 뭘까요?`
    - 멀티프로세서 시스템 :  여러 CPU → 1 시스템
    - 클러스터 시스템 : 여러 독립적 시스템 → 1 시스템 (Loosely Coupled)
    - 보통 여러 컴퓨터들이 하나의 저장소를 공유하고 LAN같은 네트워크로 연결한 시스템을 말하는 것 같아요.
        - 비대칭 클러스터링 : 여러 시스템 중 하나는 상시 대기모드로 다른 노드들을 모니터링만 합니다.
        - 대칭 클러스터링 : 두 개 이상의 노드가 작업도 수행하면서 동시에 다른 노드들을 모니터링하는 구조입니다.

---

## 6. **Operating System Structure**

- `멀티 프로그래밍` : 여러 프로그램을 메모리에 로드해두고 프로세스 대기 상태 시 다른 프로세스 작업을 수행해요.
- `시분할 (Time Sharing)`
    - 멀티태스킹이예요.
    - 프로세스마다 작업 시간 정해두고 번갈아 가면서 작업해요.
    - Response Time을 줄이는 것이 중요해요.
    - 마치 동시에 작동하는 것처럼 보이게 해요.

❗ `가상 메모리 사용`

- 너무 많은 메모리를 사용하면 Response Time을 줄이기 위해 가상 메모리를 사용해요.
- 보조 기억 장치의 일부를 마치 메인 메모리처럼 사용하는 기술이예요.

👉 `CPU 스케줄링, 작업 스케줄링`

- 이렇게 동시에 메모리에 여러 작업을 올리므로 메모리가 부족할 수 있어요.
- 이 때 어느 작업을 먼저 처리할지 고민해야합니다.

---

## 7. **Operating-System Operations**

- OS는 인터럽트 주도적이예요.
- 즉, 시스템은 인터럽트를 기다립니다.
- OS와 User는 컴퓨터 자원을 공유하기 때문에 User Program이 오류를 일으키지 않도록 방지해야 해요.

---

## 8. **Dual-Mode and Multimode Operation**

👉 User Program이 시스템에 접근하지 못하도록 Mode를 나눠요.

### Kernel Mode

- mode bit == 0
- 커널 모드일 때에만 Privileged instruction(특권 명령)을 실행해요.
- 믿을 수 있는 친구구나!

### User Mode

- mode bit == 1
- 너는 나쁜 의도를 가지고 있을 수도 있겠어.
- 순수한 친구들이 커널 모드 쓰고 싶으면 `시스템 콜`을 사용해야 해요.

---

## 9. **Timer**

- User program이 OS에게 제어권을 넘겨주지 않는 상황을 방지하기 위해 타이머를 사용해요. (혼자 독식하려는 나쁜 친구들)
- 특정 주기마다 타이머를 발생시켜 인터럽트가 발생해요.

 

---

## 10. Process Management

- on 디스크 → Program
- on 메모리 → Process
- 1프로그램이라도 多프로세스가 가능해요. (브라우저 창 여러 개 띄워두는 느낌)

---

## 11. Memory Management

---

## 12. Storage Management

### File-System Management

### Mass-Storage Management

### Caching

### I/O System

---

## 13. Protection and Security

---

## 14. Kernel Data Structures

---

## 15. Computing Environments

---

## 16. Open-Source Operating Systems
