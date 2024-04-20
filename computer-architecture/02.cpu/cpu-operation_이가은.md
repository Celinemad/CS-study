# [0416_STUDY] CPU 작동 원리

생성일: 2024년 4월 16일 오후 7:03

## 04-1 ALU와 제어장치

<aside>
💡 **CPU**         : 메모리에 저장된 명령어 읽어들임, 해석, 실행
**ALU**         : CPU 내부에서 계산 담당
**제어장치** : 명령어 읽어들이고 해석
**레지스터** : 작은 임시 저장 장치

</aside>

### ALU

![Untitled](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/3f6a4ba6-c1d7-4a11-81eb-4d10886387dd)

- **ALU가 받아들이는 정보**

  - 레지스터를 통해 **피연산자**를 받아들이고
  - 제어장치를 통해 수행할 연산을 알려주는 **제어 신호**를 받아들임

  ⇒ ALU는 이 두 가지로 산술 연산, 논리 연산 등을 수행

- **ALU가 내보내는 정보**
  1. 결괏값
     - 연산을 수행한 결과 : 숫자, 문자, 메모리 주소
     - 연산 수행 결과는 메모리에 저장되지 않고 일시적으로 레지스터에 저장됨
       - _ALU의 결괏값을 메모리가 아닌 레지스터에 우선 저장하는 이유_
         ALU가 연산할 때마다 메모리에 저장하면 CPU 접근 횟수↑
         ⇒ CPU가 프로그램 진행 속도 늦춤
  2. 플래그
     - 연산 결과에 대한 추가적인 정보
       ![Untitled 1](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/f45eae1f-bed3-403b-939b-a739dbabeaf2)
     - 플래그들은 플래그 레지스터에 저장됨
       - 연산 결과가 음수
         ![Untitled 2](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/bca4e594-2399-43c9-a2d6-cf150d8eb056)
       - 연산 결과가 0
         ![Untitled 3](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/ef5ed96d-ee36-4c4f-aa8f-06248cb276c6)
- ALU 내부의 여러 계산 & 이를 위한 회로
  - 덧셈-가산기, 뺄셈-보수기, 시프트 연산-시트퍼, 오버플로우 대비-오버플로우 검출기 등

### 제어 장치

- 제어장치
  - 제어 신호를 내보내고 명령어를 해석하는 부품
- 제어 신호
  - 컴퓨터 부품들을 관리하고 작동시키기 위한 일종의 전기 신호

![Untitled 4](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/0f100e68-7156-425d-ab67-d59bb1b1e378)

- 제어장치가 받아들이는 정보

  1. 클럭 신호
  2. 해석해야 할 명령어
  3. 플래그 레지스터 속 플래그 값
  4. 시스템 버스 중 제어버스로 전달된 제어 신호

- 제어장치가 내보내는 정보

  - CPU **외부**에 전달하는 제어 신호

    - ‘CPU 외부에 제어 신호 전달’ == ‘제어 버스로 제어 신호 내보냄’

    1. 메모리에 전달하는 제어 신호

       : 메모리에 있는 값을 읽거나 메모리에 새로운 값을 쓰고 싶을 때

    2. 입출력장치에 전달하는 제어 신호

       : 입출력장치의 값을 읽거나 입출력장치에 새로운 값을 쓰고 싶을 때

  - CPU **내부**에 전달하는 제어 신호

    1. ALU에 전달하는 제어 신호

       : 수행할 연산 지시

    2. 레지스터에 전달하는 제어 신호

       : 레지스터 간 데이터를 이동시키거나 레지스터에 저장된 명령어 해석하기 위해

## 04-2 레지스터

![Untitled 5](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/fb9c9b42-afa4-407f-97cb-dd2b7c1e69b3)

1. 프로그램 카운터
2. 명령어레지스터
3. 메모리 주소 레지스터
4. 메모리 버퍼 레지스터
5. 플래그 레지스터
6. 범용 레지스터
7. 스택 포인터
8. 베이스 레지스터

- **프로그램 카운터**

  - Program Counter, 메모리에서 가져올 명령어의 주소.
  - Instruction Pointer라고 부르는 CPU도 있음.

- **명령어 레지스터**

  - Instruction Register, 방금 메모리에서 읽어 들인 명령어를 저장.
  - 제어장치가 이 레지스터 속 명령어를 받아들이고 해석한 뒤 제어 신호를 내보냄.

- **메모리 주소 레지스터**

  - Memory Address Register, 메모리의 주소를 저장.
  - CPU가 읽어 들이고자 하는 주소 값을 주소 버스로 보낼 때 이 레지스터 거침.

- **메모리 버퍼 레지스터**

  - Memory Buffer Register, 메모리와 주고받을 값(데이터&명령어)을 저장.
  - 메모리에 쓰고 싶은 값이나 메모리부터 전달받은 값이 거치는 곳.
  - CPU가 ‘주소 버스로 내보낼 값’ = ‘주소 레지스터’
    ‘데이터 버스로 주고받을 값’ = ‘메모리 버퍼 레지스터’

- 레지스터에는 어떤 값들이 담길까

  1.  CPU로 실행할 프로그램

      ![Untitled 6](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/9a2282cf-b918-4cf3-8ee1-cc2393829966)

  1.  PC에 1000이 저장됨.
      = 메모리에서 가져올 명령어가 1000번지에 있다.

          ![Untitled 7](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/291139d0-7b0c-4c3a-b0d4-1856ec61e4ad)

  1.  1000번지를 읽어 들이기 위해 주소 버스로 1000번지 내보냄
      → 메모리 주소 레지스터에 1000 저장됨

          ![Untitled 8](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/f46300af-f768-4476-ae2c-1ecd86e253eb)

  1.  ‘메모리 읽기’ 제어신호 & 메모리 주소 레지스터 값 — 제어버스 & 주소버스 → 메모리로 보내짐

      ![Untitled 9](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/17018c65-8cf3-44c2-b32d-749e21d165ea)

  1.  메모리 1000번지에 저장된 값 — 데이터 버스 → 메모리 버퍼 레지스터로 전달됨.
      프로그램 카운터 증가.

          ![Untitled 10](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/a925ce3c-3706-442f-bd43-c464da264cfd)

  1.  메모리 버퍼 레지스터에 저장된 값 → 명령어 레지스터로 이동

      ![Untitled 11](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/c45b90d0-b279-4dc2-a02e-b07efddcccc9)

  1.  제어장치가 명령어 레지스터의 명령어를 해석하고 제어 신호 발생시킴

  ⇒ PC 지속적으로 증가 = 계속해서 다음 명령어 읽음 → CPU 프로그램 차례대로 실행

  ![Untitled 12](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/91374d07-05a2-4401-9bcd-4b7bde453465)

- **범용 레지스터**
  - general purpose register, 다양하고 일반적인 상황에서 사용할 수 있는 레지스터
  - 데이터, 주소를 모두 저장할 수 있음.
- **플래그 레지스터**
  - flag register, ALU 연산 결과에 따른 플래그를 플래그 레지스터에 저장.
  - 연산 결과 또는 CPU 상태에 대한 부가적인 정보 저장.

### 특정 레지스터를 이용한 주소 지정 방식: 스택 주소 지정 방식

<aside>
✅ 스택 포인터, 베이스 레지스터 = 주조 지정에 사용되는 레지스터
⇒ **스택 포인터**                                         : 스택 주소 지정 방식에 사용됨.
⇒ **프로그램 카운터 & 베이스 레지스터**  : 변위 주소 지정 방식에 사용됨.

</aside>

- **스택 주소 지정 방식**
  - 스택과 스택 포인터를 이용한 주소 지정 방식.
- **스택 포인터**

  ![Untitled 13](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/1c905670-05c8-41ee-a2ca-ae0b93ff162c)

  - 스택의 꼭대기를 가리키는 레지스터, 스택에 마지막으로 저장한 값의 위치를 저장.
    = ‘스택의 어디까지 데이터가 채워져 있는지에 대한 표시’

- 스택의 위치?
  ![Untitled 14](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/81907c24-b83a-4d45-acfb-3c5d58875da0)
  - 메모리 안에 스택처럼 사용할 영역이 정해져 있음. = “스택영역”
  - 다른 주소 공간과는 다르게 스택처럼 사용하기로 암묵적으로 약속된 영역

### 특정 레지스터를 이용한 주소 지정 방식(2): 변위 주소 지정 방식

- **변위 주소 지정 방식**

  - displacement addressing mode,
    오퍼랜드 필드의 값(변위) + 특정 레지스터의 값 ⇒ 유효 주소 얻어내는 주소 지정 방식
    ![Untitled 15](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/0c7d3b8a-071c-4d08-a42a-61f0b6aedbdd)
  - 변위 주소 지정 방식을 사용하는 명령어 구조
    ![Untitled 16](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/5afc47d1-9cd7-4e02-9067-ae18f584744a)
  - 오퍼랜드 필드의 주소와 어떤 레지스터를 더하는지에 따라
    → 상대 주소 지정 방식 or 베이스 레지스터 주소 지정 방식 등으로 나뉨

- 상대 주소 지정 방식

  - relative addressing mode, 오퍼랜드와 프로그램 카운터의 값을 더해서 유효 주소를 얻는 방식
  - 오퍼랜드가 -3(음수)일 때, CPU는 읽어 들이기로 한 명령어로부터 “세 번째 이전” 번지로 이동
    ![Untitled 17](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/d1907cfa-9f1f-4286-acec-7f92200189a5)
  - 모든 코드를 실행하는 것이 아닌, 분기하여 특정 주소의 코드를 실행할 때 사용(≒if문)

- 베이스 레지스터 주소 지정 방식
  - base-register addressing mode, 오퍼랜드와 베이스 레지스터의 값을 더하여 유효 주소를 얻는 방식
  - 베이스 레지스터 = ‘기준 주소’ / 오퍼랜드 = ‘기준 주소로부터 떨어진 거리’
    ⇒ 베이스 레지스터 속 기준 주소로부터 얼마나 떨어져 있는 주소에 접근할 것인지
    ![Untitled 18](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/2429ac88-4f52-4ce7-ae91-a3a370fe6688)

## 04-3 명령어 **사이클과 인터럽트**

<aside>
💡 **명령어 사이클** : CPU가 하나의 명령어를 처리하는 정형화된 흐름. (이 흐름을 반복하며 명령어 처리)
**인터럽트**         : 이 흐름이 끊어지는 상황.

</aside>

### 명령어 사이클

- **명령어 사이클**
  | 프로그램 | 수많은 명령어로 이루어짐 |
  | ----------------- | ----------------------------- |
  | → CPU | 이 명령어들을 하나씩 실행 |
  | → 각각의 명령어들 | 일정한 주기가 반복되며 실행됨 |
  ⇒ 이 주기를 명령어 사이클이라고 함
- 명령어 사이클 구성

  1. 인출 사이클 (fetch cycle)
     - 메모리에 있는 명령어를 CPU로 가지고 오는 단계. [이 과정](https://www.notion.so/0416_STUDY-CPU-0ba08d10f7304f5fb5d336bf6cdf7bd0?pvs=21)의 2~6 단계에 해당.
  2. 실행 사이클 (execution cycle)
     - CPU로 가져온 명령어를 실행. 제어장치가 명령어 레지스터에 담긴 값을 해석하고, 제어 신호 발생시킴.

  ⇒ 프로그램을 이루는 수많은 명령어가 _(일반적으로)_ 인출과 실행 사이클을 반복하며 실행됨.

- **간접 사이클**

  - 명령어를 인출해서 CPU로 가져온 뒤, 곧바로 실행하는 경우

    ![Untitled 19](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/daa0f048-d8a5-4906-8e2a-a46c2e31a083)

  - 명령어를 CPU로 가져왔다 해도 곧바로 실행할 수 없는 경우
    - ex. 간접 주소 지정 방식
      ![Untitled 20](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/48d231cb-33ff-4b73-81ce-24ce12d28565)
    - 명령어를 실행하기 위해선 메모리 접근을 한 번 더 해야 함
      → 간접 사이클 (indirect cycle)

### 인터럽트

- 인터럽트

  - interrupt, CPU의 작업을 방해하는 신호.

  ![Untitled 21](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/4efc458b-40aa-460f-8279-5130be1357e2)

- 인터럽트의 종류

  1. 동기 인터럽트
     - synchronous interrupts, CPU에 의해 발생하는 인터럽트.
     - CPU가 명령어들을 수행하다 예상치 못한 상황에 마주쳤을 때 발생하는 인터럽트.
       ⇒ **예외** (exception) 라고 부름.
  2. 비동기 인터럽트
     - asynchronous interrupts, 주로 입출력장치에 의해 발생하는 인터럽트.
     - ex. 작업을 끝낸 프린터가 CPU에 완료 알림(인터럽트)을 보냄
       키보드나 마우스가 어떠한 입력을 받았을 때 CPU에 입력 알림(인터럽트)을 보냄
     - 일반적으로 ‘비동기 인터럽트 = 인터럽트’로 칭함 (혼동방지를 위해, 이하 하드웨어 인터럽트)

- 하드웨어 인터럽트

  - CPU는 입출력 작업 도중에도 **효율적으로 명령어를 처리**하기 위해, 알림과 같은 하드웨어 인터럽트 사용
    - 효율적으로 명령어 처리?
      - ex. CPU가 프린터에 출력 명령.
        - 입출력장치는 CPU보다 속도가 현저히 느림 → CPU는 입출력 작업의 결과를 바로 받을 수 없음.
        - 하드웨어 인터럽트 사용하지 않는다면?
          - 주기적으로 프린터 완료여부 확인 → CPU 사이클 낭비
        - 하드웨어 인터럽트 사용하면?
          - CPU는 프린터로부터 프린트 완료 인터럽트를 받을 때까지 다른 작업 처리 가능

- 하드웨어 인터럽트 처리 순서

  1. 입출력장치는 CPU에 **[인터럽트 요청 신호](https://www.notion.so/0416_STUDY-CPU-0ba08d10f7304f5fb5d336bf6cdf7bd0?pvs=21)**를 보냄
  2. CPU는 실행 사이클이 끝나고 명령어를 인출하기 전 항상 인터럽트 여부를 확인함
  3. CPU는 인터럽트 요청을 확인하고 **[인터럽트 플래그](ssafy%20d5ef03864d57459499cbf229069a72e2/SSAFY%20Java%20Note%20e0ca85d108584dd1a8daa39b0b917b52.md)**를 통해 현재 인터럽트를 받아들일 수 있는지 여부 확인
  4. 인터럽트를 받아들일 수 있으면 CPU는 지금까지의 작업을 백업함
  5. CPU는 **[인터럽트 벡터](https://www.notion.so/0416_STUDY-CPU-0ba08d10f7304f5fb5d336bf6cdf7bd0?pvs=21)**를 참조하여 **[인터럽트 서비스 루틴](https://www.notion.so/0416_STUDY-CPU-0ba08d10f7304f5fb5d336bf6cdf7bd0?pvs=21)**을 실행
  6. 인터럽트 서비스 루틴이 끝나면 (4.)에서 백업해둔 작업을 복구하여 실행 재개

  - **인터럽트 요청 신호**
    - CPU의 정상적인 실행흐름을 끊기 전, 끼어들어도 되는지 CPU에 물어보는 행위
    - 인터럽트 요청을 수행하기 위해선 플래그 레지스터의 인터럽트 플래그가 활성화되어 있어야 함.
      ![Untitled 22](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/2981aff2-12b4-45cf-a333-341690de1276)
  - **인터럽트 플래그 (interrupt flag)**
    - 하드웨어 인터럽트를 받아들일지, 무시할지 결정하는 플래그
    - ‘불가능’ → 인터럽트 요청이 와도 CPU는 이를 무시 / ‘가능’ → 인터럽트 처리
    - 인터럽트 플래그가 ‘불가능’이어도 무시할 수 없는 인터럽트 요청
      - 가장 먼저 처리해야 하는 인터럽트 (ex. 정전, 하드웨어 고장..)
        ![Untitled 23](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/750b9b07-619d-4c23-bff3-625622517cb9)
    - CPU가 인터럽트 요청을 받아들이기로 하면 인터럽트 서비스 루틴 실행
  - **인터럽트 서비스 루틴 (ISR; Interrupt Service Routine)**

    - 인터럽트를 처리하기 위한 프로그램.
    - 인터럽트 핸들러 (interrupt handler)라고도 부름.
    - 어떤 인터럽트가 발생했을 때, 해당 인터럽트를 어떻게 처리&작동해야 할지에 대한 정보로 이루어진 프로그램

  - **인터럽트 벡터 (interrupt vector)**

    - CPU는 수많은 인터럽트 서비스 루틴을 구분하기 위해 인터럽트 벡터 이용. (인터럽트 서비스 루틴 식별 정보)
      - 인터럽트 백터 : 인터럽트 서비스 루틴의 시작 주소 알 수 있음 → 인터럽트 서비스 루틴 처음부터 실행
    - _‘CPU가 인터럽트 처리’ == ‘인터럽트 서비스 루틴 실행 후, 본래 수행하던 작업으로 컴백’_
      ![Untitled 24](https://github.com/Ssafy-Developer-Study/CS-study/assets/48985475/16f3cb86-f59a-4543-9449-ac86e5dc361a)

      1. 정상적으로 작업 진행
      2. 인터럽트 발생
      3. 인터럽트 서비스 루틴으로 점프
      4. 인터럽트 서비스 루틴 실행
      5. 기존 작업으로 점프
      6. 기존 작업 수행 재개

      - 인터럽트 처리 방법은 입출력장치마다 다름 = 각기 다른 인터럽트 서비스 루틴 가짐
        (위 그림과 같이 메모리에 여러 개의 ISR↓ 저장되어 있음)
      - 이 여러 ISR을 구분하기 위한 것이 인터럽트 벡터
