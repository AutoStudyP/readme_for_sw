  ## 과제 내용: 리눅스 명령어와 vim 에디터에서 메크로 관련하여 조사하기
  *  리눅스 명령어: top ,ps ,jobs ,kill 명령어 조사하기
  *  vim 에디터에서 메크로 사용방법에 대하여 조사하기(q,@)

# 과제01
## 01. process

1. top - display tasks
2. ps - Reprot a snapshot of current processes
3. jobs - List active jobs
4. kill - send a signal to a process

## 02. each info

### 01. TOP : 시스템 프로세스/메모리 사용 현황을 실시간으로 출력한다.

사용법 : &top[옵션]

옵션|의미|
---|---|
-n|지정한 숫자만큼 화면 출력을 갱신|
-u|지정한 사용자의 프로세스를 모니터링|
-b|출력결과를 파일이나 다른 프로그램으로 전달|
-d|화면갱신주기를 초 단위로 설정|
-p|지정한 PID 프로세스를 모니터링






![top process](https://user-images.githubusercontent.com/97014059/169685951-622b7963-9337-4db8-b3be-8809041514ba.png)

**$ps** 명령어는 명령어가 실행된 순간의 프로세스 상태들에 대해서 **정적인 정보**만을 제공하며,
**$top**은 **시스템 활동을 실시간**으로 확인할 수 있다.
top 프로그램은 **활동 순으로 나열된 프로세스들을 지속적으로 갱신** 하면서 보여준다.

**위쪽**은 시스템에 대한 **전반적인 요약**을 보여주며,
**아래**는 테이블로써 **CPU를 사용하는 순으로 프로세스들을 정렬**해서 보여준다.

>**시스템 요약 부분 항목**
> * 첫째줄 - 현재시간, 서버가동 후 유지시간, 현재 접속 사용자, 최근 1, 5, 15분 동안 시스템 부하
> * 둘째줄 - 프로세스의 상태(총 프로세스, 실행중, sleep, stop, 좀비프로세스)
> * 셋째줄 - cpu상태
> * 넷째줄 - MEM 상태
> * 다섯째줄 - swap 메모리 상태

>**프로세스 cpu 사용 순서 부분 항목**
> * PR - 우선순위 부하
> * NI - Nice value(-20~19 사이의 숫자이며 값이 작을수록 우선순위가 높음) 
> * VIRT - 작업에 사용된 가상 메모리 총사용량 
> * RES - 프로세스가 사용하는 실제 메모리양
> * SHR - 프로세스가 사용하는 공유 메모리양
> * 현재 프로세스의 상태를 나타냄
> * TIME+ - 프로세스가 시작하여 사용한 CPU시간

top을 통해 모니터링 중인 상태에서 h 를 누르면 다양한 추가적인 기능들에 대한 도움말을 볼 수 있다.
top 역시 하나의 프로세스가 되기 때문에 top 의 결과에서 top 프로세스도 같이 등장하며, 시스템 리소스를 굉장히 적게 사용하기 때문에 시스템 부하를 적게 일으키는 좋은 프로그램이다.

### 02. ps(프로세스 출력)
리눅스는 다중 사용자, 사용 작업 시스템이기 때문에 여러 개의 프로세스를 동시에 수행하기 때문에 항상 어떤 프로세스들이 실행되고 있는지 모니터링할 필요가 있다. 
따라서 현재 시스템에서 실행 중인 프로세스에 관한 정보를 출력하여 사용자에게 정보를 제공하는 명령어가 필요한데 이때 사용하는 명령어가 ps이다.

윈도우에서 특정 프로세스가 실행 중인지 확인하거나 강제 종료하기 위해 **작업 관리자**를 사용하듯이,
리눅스에서는 **ps 명령어**가 자주 사용된다.
특히 GUI를 사용하지 않는 서버 환경에서는 대부분의 프로세스들이 백그라운드에서 동작하기 때문에 특정 프로세스가 동작 중인지 확인하기 위해서 많이 쓰인다.

> bash 스크립트(script)를 통한 자동화에도 ps 명령어가 자주 사용되는데,
주로 특정 프로세스에 시그널(signal)을 보내야 할 때 PID(process id)를 식별하기 위해서 쓰이기도 하고, 프로세스가 중단되면 다시 실행시키기 위해 감시하는 목적으로 쓰이기도 한다. 

사용법 : &ps[옵션]

**기본** 프로세스 출력:
- a:터미널과 **연관된** 프로세스만 출력
- x: 터미널과 **연관되지 않은** 프로세스만 출력
- -A: 모든 프로세스 출력(-e와 동일)
- -e: 모든 프로세스 출력
- -a: 세션 리더와 터미널과 연관되지 않은 프로세스를 출력

**지정한**프로세스 출력:
- p: **지정한 PID** 목록의 정보만 출력
- -C: 지정한 프로세스의 실행 파일 이름의 정보만 출력
- -u: 특정 사용자의 프로세스 정보를 출력

프로세스 **표시형식**
- u: 프로세스의 **소유자 정보**를 함께 출력
- i: BSD 형식의 긴 형식으로 출력
- e: 프로세스 정보와 함께 프로세스의 환경변수 정보도 출력
- -i: 긴포맷으로 출력
- -o: 사용자 정의 형식 지정 가능

프로세스 **장식**
- f: 프로세스 계층을 텍스트 형식의 트리구조를 보여줌
- -f: 전체 포맷으로 출력





![sw (ps)](https://user-images.githubusercontent.com/97014059/169686755-e95a83b6-51b5-480b-956e-789b3079ebca.png)



프로세스 항목|의미|
---|---|
-F|	프로세스 플래그|
-S|프로세스 상태코드|
-UID|프로세스 소유자이름|
-PID|프로세스 고유식별자|
-PPID|부모프로세스의 PID|
-C|프로세서 사용률 %로 표기|
-PRI|	프로세스의 우선순위. 높은값이 낮은 우선순위|
-NI|nice 값이며 19에서 -20값|
-SZ|프로세스 이미지가 차지하는 물리적 페이지 크기|
-WCHAN|대기중일때 커널 함수의 이름|
-STIME|프로세스가 시작한 시간|
-TTY|터미널의 종류|
-TIME|총 CPU 사용시간|
-CMD|프로세스의 실행 시 명령줄|


### 03. jobs(백그라운드 프로세스 출력)
jobs 명령어는 현재 돌아가고 있는 **백그라운드 프로세스 리스트를 모두 출력**해준다.
백그라운드 프로세스는 스택처럼 쌓이는데,
 **+는 스택의 가장 위**에 있다는 뜻이고
 **-는 바로 그다음 밑**에 있다는 뜻이다.

사용법 : &jobs[옵션][job name or number]




![jobs sw](https://user-images.githubusercontent.com/97014059/169687706-ad057a5b-21cb-440e-9792-c3299392b2ee.png)


### 04. kill(시그널-프로세스 종료)
시그널은 프로세스 사이의 통신 수단인데 어떤 프로세스에 메시지를 보내 프로세스를 제어한다.

명령어를 실행함으로써 프로세스가 시작되고 그 프로세를 제어하기 위하여 사전에 정의된 시그널이 존재한다.

![kill](https://user-images.githubusercontent.com/97014059/169687791-90cd6617-0a9c-444d-8c9d-6a1eff0d6461.png)


번호|시그널|의미|
---|---|---|
1|SIGHUP|	 터미널에서 접속이 끊겼을때 보내지는 시그널, 변화된 내용을 적용하기 위해 재시작 할 때 사용된다. |
2|SIGINT|인터럽트 시그널로 실행을 중지시킴, Ctrl + c 입력시 보내지는 시그널|
3|SIGOUIT|실행 중지 시그널로서 Ctrl + \ 입력시 보내지는 시그널|
9|SIGKILL|프로세스를 강제로 종료 시키는 시그널|
15|SIGTERM|kill의 기본 시그널로 정상 종료 시키는 시그널|
18|SIGCONT|시그널에 의해 정지된 프로세스를 다시 실행시키는 시그널|
19|SIGSTOP|	정지 시그널 |
20|SIGTSTP|일시정지 시키는 시그널로서 Ctrl + z 입력시 보내지는 시그널|

위의 경우처럼 몇 가지 시그널이 존재하는데 **불필요한 프로세스, 잘못 실행된 프로세스를 죽이는데 사용할 것은** KILL이있다.

kill 명령어는 프로세스를 강제로 종료시킨다. 좀비 프로세스나, 응답 없음, 비정상적으로 동작하는 프로세스들의 실행을 끝내게 해준다.

프로세스를 포어그라운드로 가져와서 ctrl + C 할 수도 있지만, **PID 를 확인하여 kill 로 바로 종료**시킬 수도 있다.
]


![KILL2](https://user-images.githubusercontent.com/97014059/169688089-98e3f76d-f395-4627-804c-31d12309f340.png)

옵션|의미|
---|---|
-signal,-s signal|지정한 시그널을 보냄 |
-l|사용 가능한 시그널의 목록을 출력|


![KILL3](https://user-images.githubusercontent.com/97014059/169688090-5a96ddbb-a5e0-4dc8-90bd-058eaff6f847.png)


**프로세스 여러개 종료 (killall)**
지정한 이름에 부합하는 모든 프로세스에게 시그널을 보낸다.

시그널을 지정하지 않으면 SIGTERM(15) 전송한다.

지정한 프로세스 이름에 매칭되는 프로세스가 모두 종료되므로 여러 프로세스를 띄우고 있는 데몬을 종료할 때 유용하다.

**프로세스 필터 종료 (pkill)**
프로세스 이름과 지정한 패턴이 부합하는 프로세스만을 종료


# 과제 02

## vi / vim / gvim 에서 매크로 사용하기

### (1) 기본적인 매크로 사용 방법
커맨드 모드 (esc 누른 상태) 에서.
1. 'q' 를 누르고 a~z 사이 문자로 매크로 recording 시작
2. 커맨드 모드로 돌아와서 'q'를 누르면 매크로 recording 끝
3. 매크로를 사용하려면 커맨드 모드에서 @+a~z 를 입력하면 됨

### (2) 자주 사용하는 매크로 등록 방법
1. ~/.vimrc 를 연다.
2. let @a = '매크로 문자열'    // 이런 식으로 매크로로 동작시킬 문자열을 입력한다.

 

### (3) 매크로 문자열을 편집기에 그대로 출력하는 방법
- 첫 번째 방법: 편집 모드에서 ctrl + r, ctrl + r, 매크로 문자  를 순서대로 입력하면 그대로 출력된다.
- 두 번째 방법: 커맨드 모드에서 "매크로문자p 를 입력하여 래지스터로부터 바로 붙여넣기 한다. (ex: "ap, "bp, "cp, "dp, ...)

 첫 번째 방법은 방향키 등의 특수키 문자가 제대로 붙여넣기가 되지 않는다.
분명히 출력 결과물이 같아 보이지만 실제 바이너리를 뜯어보면 다르게 출력됨을 알 수 있다.

#####
