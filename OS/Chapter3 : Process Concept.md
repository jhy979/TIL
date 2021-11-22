## 1. Process State

- 프로세스
    - on 디스크는 프로그램, on 메모리는 프로세스라고 합니다.
    - 알다시피 stack heap data text 로 나뉩니다.'
- 프로세스의 상태
    - New
    - Ready
    - Running
    - Waiting
    - Terminated

---

## 2. Process Control Block (PCB)

- `PCB`
    - 각 각의 프로세스는 자신의 정보 묶음인 PCB를 가지고 있어요.
    - Process 정보, 레지스터, 스케쥴링, 메모리, I/O 등...
- 어떠한 정보들?
    - Process State : 프로세스 상태
    - Program counter : 다음 명령 주소
    - CPU registers : 프로세스가 인터럽트 이후 올바르게 작업을 이어가기 위해 참조하는 CPU 레지스터 값
    - CPU-scheduling information : 스케쥴링과 관련된 정보 (중요도, 스케줄링 큐 포인터)
    - Memory-management information : base, limit 레지스터 값, 페이지 테이블 등의 메모리 시스템 정보
    - Accounting information : 사용된 CPU 총량, 프로세스 개수, 시간 제한 등
    - I/O status information : 프로세스에 할당된 I/O device 목록, 열린 파일 목록 등

---

## 3. Threads

- 프로세스를 쪼개 `하나의 프로세스 안에서 동시에 여러 작업`을 처리할 수 있어요.
- 싱글 스레드 프로세스는 한 번에 하나의 작업만 할 수 있어요.

---

## 4. Process Scheduling

- 멀티 프로그래밍의 목적
    - `CPU를 최대 사용`하고 싶어요! → 항상 일부 프로세스를 실행
- 타임 쉐어링의 목적
    - 프로세스 간 CPU를 자주 전환 → `사용자`가 각 프로그램이 실행되는 동안 `서로 상호작용`할 수 있도록!

👉 멀티 프로그래밍과 타임 쉐어링의 목적을 위해 CPU에서 실행 가능한 프로세스를 선택하고 할당하는 일을 프로세스 스케쥴링이라 합니다.

### Scheduling Queues

- Job Queue
    - 프로세스가 시스템에 들어오면 잡 큐로 들어갑니다.
- Ready Queue
    - 메인 메모리에서 실행을 기다리는 ready 상태의 프로세스들
- Device Queue
    - 입출력 장치를 기다리는 프로세스들

### Schedulers

- `Job Scheduler , Long-term Scheduler`
    - to ready queue
    - CPU 밖에서 가끔 수행됩니다.
- `CPU Scheduler , Short-term Scheduler`
    - to processor
    - CPU 안에서 자주 수행됩니다.

---

## 5. Context Switch

- 프로세스 실행 도중 문제 발생 → 인터럽트 발생 → OS가 개입하여 할당된 `프로세스를 교체! (프로세서가 현재 가지고 있는 PCB의 정보가 바뀌겠죠?)`
- Syscall을 사용해야 하면 프로세스가 자체적으로 처리할 수 없기 때문에 OS가 개입해야 해요.
- `Context` : 내 시스템에서 활용 가능한 모니터링된 정보들
    - 프로세서 입장에서는 Context == PCB 이기 때문에 결국 PCB 정보가 바뀌는 것을 컨텍스트 스위치라고 부르는 겁니다.

🤔 하지만, Context Switch는 오버헤드가 발생하니 자주 하면 안 됩니다! 

---

## 6. Operations on Processes

- 시스템은 프로세스 생성, 삭제 메커니즘을 제공해야 해요.

### Process Creation

🎄 프로세스는 트리 구조 

🔑 PCB의 pid로 식별합니다.

🔨 생성은 마치 `플라나리아 번식` 

- 부모가 fork()로 자식을 생성해요.
- 자식은 exec()로 내용을 변경해요.

❗ fork()를 하게 되면 부모는 자식의 pid를 가지게 되고 자식은 0을 가지게 됩니다.

- 부모와 자식은 동시에 작동해요.

### Process Termination

🔚 exit()를 호출하면 프로세스가 종료됩니다.

🧑‍🍼 부모 종료 → 자식은 상위 프로세스를 부모로 봅니다 (할아버지, 할머니)

😂 자식 종료 → 만약 부모가 자식이 반환한 정보를 회수하지 않았다면 자식은 좀비가 됩니다. (정보가 메모리에 남아 있는 상태)

- Orphan, Zombie

---

## 7. Interprocess Communication (IPC)

- 프로세스 간 통신을 말합니다. 어떻게 프로세스간 통신이 일어날까요?

### Message Passing

📫 우편 방식

- 송신 → `커널` → 수신

😀 커널에서 기본적인 기능을 제공해서 구현이 쉬운 편이예요.

😂 Context Switching이 발생해서 `느려요!`

### Shared Memory

📄 게시판 방식

- 특정 메모리 공간을 프로세스가 함께 사용하며 정보를 주고 받습니다.

😀커널 없어서 빨라요.

😂 메모리 동시 접근을 막아야해서 프로그래머가 더 구현해줘야 해요.

### Producer-Consumer Problem

- 생산자 - 소비자 문제
    - 프로세스 중 정보를 생산하는 친구를 생산자, 받는 친구를 소비자라고 해요.
    - `생산보다 소비가 빠르면` 동기화 문제가 발생해요.
    
    🤔 `버퍼`를 사용합시다.
    

### Synchronization

- `Message Passing Sync 문제 해결 방법`
    - Blocking 방식
        - Blocking Send : 수신자 받을 때까지 송신자 멈춰!
        - Blocking Receive : 메시지 받을 때까지 수신자도 멈춰!
    - Non-blocking 방식
        - Non-blocking Send : 메시지 보내고 송신자 알아서 해!
        - Non-blocking Receive : 수신자가 유효 or null 메세지를 받아요.

---

## 8. Sockets

↔ 서버와 클라이언트가 통신하는 방식이예요.

- `ip 주소, 포트 정보`만 있다면.. →  클라가 서버에 접근 가능해요.
- `RPC(Remote Procedure Calls)`
    - 프로세스와 프로세스가 네트워크로 이어져 있을 때 발생하는 호출이예요.
    - 서버와 클라이언트가 통신할 때는 `IP주소와 포트를 래핑해서 Stub`으로 만들어 전송합니다.

---

## 9. Pipes

- 부모와 자식 프로세스가 통신할 때 사용하는 방식이예요.
- 프로세스 사이에 파이프를 두는 거죠!

😕 파이프는 단방향 통신이라 양방향 하려면 두 개 필요해요.

- `파이프는 파일입니다.`
- 파이프에 이름을 붙인 named pipe를 사용하면 부모-자식 관계 아니여도 통신이 가능해요.
