# OS Chapter2: 시스템 구조

## 1. Operating-System Services

User | GUI, batch, command line | user interfaces | system calls | `services` | OS | hardware

- `UI (User Interface)`
    - 사용자와 컴퓨터 시스템이 만나는 지점이예요.
    - Batch Interface : 명령을 파일에 넣어두고 실행하면 명령이 실행되는 인터페이스예요. (배치파일)
    - CLI : 알죠?
    - GUI : 알죠?
- `Program Execution`
    - 프로그램 → 메모리에 로드 → 실행
- `I/O operation`
    - 프로그램에서 입출력 필요하면 효율과 보안을 위해 OS를 거쳐 입출력 장치를 조작해요.
- `File-system manipulation`
    - 파일 Write, Read, Create, Delete, 접근 제어
- `Communication`
    - 프로세스 간 정보 교환을 담당합니다.
    - 기법으로는 Shared Memory, Message Passing이 존재해요.
    - Message Passing 이 당연히 더 느리겠죠?
- `Error Detection`
    - CPU, Memory, 입출력 장치, 프로그램 등에서의 에러를 탐지하고 수정해요.
- `Resource Allocation`
    - 여러 사용자, 작업을 동시 처리해야하면 컴퓨팅 자원을 잘 분배해야 합니다.
- `Accounting`
    - 어떤 유저가 어떤 자원을 사용하고 있는지 감시해요.
- `Protection and Security`
    - 보안은 늘 중요하죠.

---

## 2. System Calls

```jsx
커널↔사용자 프로그램 이어주는 인터페이스예요.
		User Application
User mode
		System call Interface
Kernel mode
```

😀 예를 들어볼까요?

1. 사용자 프로그램이 디스크에 있는 파일을 열고 싶어요 (즉, 파일 시스템에 접근 원해요.)
2. Kernel Mode로 전환해야겠죠? 이 때 System call을 사용해요.
3. `fopen()` 함수를 호출한다면 OS는 `시스템 콜 테이블(or 인터럽트 벡터)`를 참조해요.
4. 시스템 콜 테이블은 메모리 주소의 모음이고, 각 각의 메모리 주소는 `인터럽트 서비스 루틴`을 가르키고 있어요. (인터럽트 서비스 루틴은 보통 C로 짜여진 코드예요.)

```jsx
fopen() -> System Call Table 체크 -> Table 속에서 `인터럽트 서비스 루틴`을 실행해요.
```

- 시스템 콜의 예시로는 fork(), exit(), read(), write() 같은 함수들이 있어요.
- 하지만 사용자가 직접 호출하는 것은 위험하고 불편하니깐 표준 라이브러리(Standard library)를 사용해요. `stdio.h`가 그 일종이예요.

### User Prog → OS 매개 변수를 넘기는 방법 3가지

1. Call by Value 
2. Call by Reference
3. 프로그램을 통해 Stack에 매개변수를 추가하고 OS를 통해 값을 빼는 방식

---

## 3. Types of System Calls

- 크게 6개로 분류할 수 있어요. (프파장정통보)
1. 프로세스 제어
    - end, abort, load, execute
2. 파일 관리
    - create, delete, open, close, read, write
3. 장치 관리
    - read, write, request, release
4. 정보 유지
    - get / set time or date
5. 통신
    - send / receive messages, transfer status
6. 보호

---

## 4. Operating System Structure

👉 현대 OS는 계층을 나눠서 시스템을 관리해요.

### Simple Structure

1. MS-DOS
- Microsoft에서 개발한 윈도우 이전 처음으로 사용화된 OS입니다.
- No 계층 분리
- User Prog가 직접 입출력 루틴에 접근해 쓰기 작업을 했어요.
- 따라서, User Prog가 고장나면 전체 System이 문제가 생겨요.
1. UNIX
- 범용 다중 사용자 방식의 대화식, 시분할처리 시스템용 OS예요.
- MS-DOS보다는 기능이 많이 분리되었지만, 여전히... Too much
- Monolithic 구조 : 구현, 유지보수가 어려워요.

---

### Layered Approach

- OS를 `더 세분화해 계층을 분리`한 것이 계층적 접근 방식이예요.
- Layer N → 0 : 0이 하드웨어이고, N이 User Interface입니다.
- 유지보수에 굉장히 유리해요.

---

### Micro kernels

- 핵심적 요소만 남긴 `가벼운 커널`이예요.
- 단점
    - 유지보수가 좋아요.
    - 컴파일, 테스트 시간이 짧아요.
    - 이식성이 좋아요.
- 단점
    - 시스템 프로그램을 추가해 기능을 늘리려고하면 속도가 느려져요.

---

### Modules

- `커널을 확장`하는 기술이예요. (마치 OOP에서 말하는 모듈화)
- 프로세스에 실시간으로 모듈을 붙여 작동시킬 수 있어요.
- 각 기능들을 독립적으로 관리할 수 있어요.
- 장치 드라이버는 모두 모듈로 구현되어 있다는 사실!
    - `.dll` 파일이 모듈이예요.

---

### Hybrid Systems

- `스마트폰`은 OS 구조의 최신판
- `커널의 핵심만 남긴 것`이 하이브리드 시스템이예요.
- 나머지는 따로 구현
- iOS : BSD가 핵심, 나머지는 모두 애플이 자체 구현
- Android : 리눅스가 핵심, 자체 구현한 라이브러리
