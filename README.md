리눅스 명령어
=============
1.top
-------------
시스템의 현재 OS의 상태에 대한 정보를 가장 빠르게 파악할 수 있는 명령어
> CPU 사용량, 메모리 사용량, 프로세스의 상태 등을 모니터링

* top 명령어 실행
  * top을 실행 -> 터미널 화면에 실시간으로 화면을 갱신하며 정보를 보여줌

* 화면 구성
  * top: 시스템 전반적인 정보를 표시. (로드 평균, 실행 중인 프로세스 수, CPU 및 메모리 사용량)
  * middle: 실행 중인 프로세스 목록을 표시. (ID, CPU 사용량, 메모리 사용량, 실행 시간)
  * bottom: 사용자 입력을 받는 메뉴

* 명령어 입력

| 명령어 | 내용 |
| --: | :-- |
| __h__ | 도움말을 표시 |
| __k__ | 프로세스를 종료하기 위해 프로세스 ID를 입력받음 |
| __r__ | 프로세스의 우선순위를 변경하기 위해 PID와 우선순위 값을 입력받음 |
| __q__ | top을 종료 |

* 정렬

| 명령어 | 내용 |
| --: | :-- |
| __P__ | CPU 사용량에 따라 정렬 |
| __M__ | 메모리 사용량에 따라 정렬 |
| __T__ | 실행 시간에 따라 정렬 |

* CPU 사용량

| 요소 | 내용 |
| --: | :-- |
| us | 프로세스의 유저 영역에서의 CPU 사용률 |
| sy | 프로세스의 커널 영역에서의 CPU 사용률 |
| ni | 프로세스의 우선순위(priority) 설정에 사용하는 CPU 사용률 |
| id | 사용하고 있지 않는 비율 |
| wa | IO가 완료될때까지 기다리고 있는 CPU 비율 |
| hi | 하드웨어 인터럽트에 사용되는 CPU 사용률 |
| us | CPU 사용량에 따라 정렬 |
| si | 소프트웨어 인터럽트에 사용되는 CPU 사용률 |
| st | CPU를 VM에서 사용하여 대기하는 CPU 비율 |

* 메모리 사용량
  * total : 총 메모리 양
  * free : 사용가능한 메모리 양
  * used : 사용중인 메모리 양

* 필터링
  * __u__: 특정 사용자의 프로세스만 볼 때 사용

2.ps
-------------
*process status*의 줄인말로 현재 실행 중인 프로세스의 목록과 상태 보여줌

* __-e__: 모든 프로세스
* __-f__: 완전한 포맷
* __-l__: 긴 포맷

사용 방법 예시:

    $ ps -ef : 모든 프로세스를 풀 포맷으로 출력
    $ ps -ef | grep '프로세스명' : '프로세스명'의 프로세스 구동 확인
    
* 출력 내용

| 행 제목 | 내용 |
| --: | :-- |
| UID | 실행 유저 |
| PID | 프로세스 ID |
| PPID | 부모 프로세스 ID |
| C | CPU 사용량 |
| STIME | Start Time |
| TTY | 프로세스 제어 위치 |
| TIME | 구동 시간 |
| CMD | 실행 명령어 |

* BSD 계열 옵션

| 옵션 | 내용 |
| --: | :-- |
| a | 모든 사용자 |
| u | 프로세스의 사용자 / 소유자 |
| x | 데몬 프로세스 |
| f | 프로세스 상속관계 트리구조로 출력 |
| ww | 넓게(wide) |

사용 방법 예시:

    $ ps aux : 실행 중인 모든 프로세스 확인
    $ ps auxf : 실행 중인 프로세스를 트리구조로 보여줌
    $ ps auxfww : 실행 중인 프로세스를 트리구조 + 모든 실행 중인 옵션 확인 
    
3.jods
-------------    
백그라운드로 실행되고 있는 프로세스를 조회하는 명령어
> 사용법 : jobs [option]

* 옵션
  * __-p__: 백그란운드에 있는 프로세스의 프로세스 아이디(PID)만 출력
  * __-l__: 백그라운드에 있는 프로세스의 프로세스 아이디(PID)를 함께 출력
  * __-s__: 백그라운드에 있는 프로세스 중 멈춰있는 프로세스만 출력
  * __-r__: 백그라운드에 있는 프로세스 중 실행중인 프로세스만 출력
  * __command__ : 지정한 명령어를 실행

사용 방법 예시:

    $ [15:51:12 oss]$ jobs
    [1]   Stopped                 vi
    [2]-  Stopped                 vi
    [3]+  Stopped                 vi

* 상태값

| 옵션 | 내용 |
| --: | :-- |
| Running | 작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중임을 의미 |
| Done | 작업이 완료되어 0을 반환하고 종료했음을 의미 |
| Done (code) | 작업이 정상적으로 완료했으며, 0이 아닌 코드를 반환했음을 의미 |
| Stopped | 작업이 일시 중단됨을 의미 |
| Stopped (SIGTSTP) | SIGTSTP 신호가 작업을 일시 중단했음을 의미 |
| Stopped (SIGSTOP) | SIGSTOP 신호가 일시 중단했음을 의미 |
| Stopped (SIGTTIN) | SIGTTIN 신호가 작업을 일시 중단했음을 의미 |
| Stopped (SIGTTOU) | SIGTTOU 신호가 작업을 일시 중단했음을 의미 |


4.kill
-------------    
프로세스에 특정한 signal을 보내는 명령어

1)시그널을 지정하지 않을 경우 기본 값인 정상 종료 시그널을 보냄

    $ kill [pid]

2)시그널 지정

    $ kill -s [signal id] [pid]
    $ kill -s [signal text] [pid]
    $ kill -[signal id] [pid]
    $ kill -[signal text] [pid]
    
* 시그널 

| 옵션 | 내용 |
| --: | :-- |
| Ctrl+c | 실행중인 프로세스에 SIGINT신호를 보냄(프로세스 종료) |
| Ctrl+z | 행중인 프로세스에 SIGITSTP신호를 보냄(프로세스 정지) |
| Ctrl+￦ | 실행중인 프로세스에 SIGINT신호를 보냄(프로세스 종료 + 코어 덤프) |

* 시그널 종류
---------------------------------------
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX
---------------------------------------

_자주 사용하는 시그널 = 1(SIGHUP), 2(SIGINT), 3(SIGQUIT), 9(SIGKILL), 15(SIGTERM), 18(SIGTSTP), 19(SIGCONT), 20(SIGCHLD)_
    



    
















