GNU

GPL





/ 가 root

- 관리자 로그인 
  - 아이디 : root
  - 비밀번호 : gong073100

Terminal을 실행 

- 종료

  - shutdown -P now
  - halt -p
  - init 0   (reunlevel)
    - 0 : 종료
    - 6 : 다시 시작

- 재시작

  - shutdown -r now
  - reboot
  - init 6

- 로그아웃

  - exit
  - logout

- 가상콘솔 : 최대 6개의 사용자로 로그인 가능

  - Ctrl + Alt+F1 : x 윈도우 
  - Ctrl + Alt+F2 : 다른 사용자로 로그인
  - Ctrl + Alt+F3
  - Ctrl + Alt+F4
  - Ctrl + Alt+F5
  - Ctrl + Alt+F6

- RunLevel : init 명령어 뒤에 붙는 숫자의 의미 

  ​				: RunLevel 숫자마다 의미가 정해져 있다.

  - 0 : 종료모드
  - 1 : 시스템 복구모드
  - 2 - 4 : Text 기반 다중 사용자 모드
  - 5 : 그래픽 기반 다중 사용자 모드
  - 6 : reboot

- pwd : print working directory

  ​		: 현재 작업하고 있는 디렉토리의 경로 

- cd : change directory

- Terminal 을 실행 시킨 후 working directory를 /lib/systemd/system 에 들어가면 RunLevel에 대한 정보를 확인할 수 있다.

- ls (list) : 현재 디렉토리 안의 파일이나 디렉토리 목록을 출력

  - ls -al : 상세한 정보 포함 출력
  - ls -al runlevel*: RunLevel이라는 글자로 시작하는 것만 필터링해서 출력

- /lib/systemd/system 안의 RunLevel*(RunLevel이라고 시작하는 모든 파일과 디렉토리)을 ls로 출력

![1561536402065](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561536402065.png)

- RunLevel 0~6이 특정 타겟을 지칭함 

- 첫 부팅 시, RunLevel 5로 실행 

  => 첫 부팅 시 어떤 RunLevel로 실행할지를 지칭하는 파일(링크 = 바로가기 아이콘 name=default.target)

  => /etc/systemd/system/default.target

  ![1561536707846](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561536707846.png)

  - 해당 링크를 다른 타깃으로 변경

    - ln-sf (심볼릭 링크를 만드는 것 )	/lib/systemd/system/multi-user.target(지칭되는 곳=/lib/systemd/system= 실제로 RunLevel이 있는 곳)   /etc/systemd/system/default.target (어디에 어떤 이름의 링크를 만들지)

    - ln   -sf   /lib/systemd/system/multi-user.target   /etc/systemd/system/default.target 

      : 부팅 시, text 기반 

    - ln   -sf   /lib/systemd/system/graphical.target   /etc/systemd/system/default.target 

      : 부팅 시, graphic 기반 
