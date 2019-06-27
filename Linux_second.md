GNU

GPL





/ 가 root



## Linux 기본 명령어

- 관리자 로그인 
  - 아이디 : root
  - 비밀번호 : gong073100

Terminal을 실행 

- 종료

  - #shutdown -P  now
  - #halt -p
  - #init 0   (reunlevel)
    - 0 : 종료
    - 6 : 다시 시작

- 재시작

  - #shutdown -r now
  - #reboot
  - #init 6

- 로그아웃

  - #exit
  - #logout

- 가상콘솔 : 최대 6개의 사용자로 로그인 가능

  - Ctrl + Alt+F1 : x 윈도우 
  - Ctrl + Alt+F2 : 다른 사용자로 로그인 - Text 기반
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

  - #cd : 바로 홈 디렉토리로 이동

- Terminal 을 실행 시킨 후 working directory를 /lib/systemd/system 에 들어가면 RunLevel에 대한 정보를 확인할 수 있다.

- ls (list) : 현재 디렉토리 안의 파일이나 디렉토리 목록을 출력

  - #ls : 숨김(.으로 시작하는 파일) 파일이나 디렉토리는 제외하고 출력

    <옵션>

  - #ls -a : 숨김파일까지 포함해서 모든 파일을 출력

  - #ls -l : 상세한 정보 출력 (퍼미션, 소유자, 그룹. 파일크기 등)

  - #ls -al : 숨김 파일까지 포함한 상세한 정보 포함 출력
  - #ls -al runlevel*: runlevel이라는 글자로 시작하는 것만 필터링해서 출력

- cat : 해당 파일의 내용을 확인할 때

  - #cat 파일명 
    - #cat anaconda-kr.cfg == #cat anacon[Tab]
      - 만약, anacon으로 시작하는 파일이 없거나 여러 개 있는 경우는 [Tab]을 통해 자동완성을 할 수 없다. 
      -  [Tab]을 두번 누르면, anacon으로 시작하는 모든 파일을 listing 해준다.

- 기본적인 도스키 제공 

  - 화살표 키 위, 아래를 이용해서 기존에 사용했던 명령을 다시 이용할 수 있다.

- /lib/systemd/system 안의 runlevel*(runlevel이라고 시작하는 모든 파일과 디렉토리)을 ls로 출력한다.

![1561536402065](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561536402065.png)

- RunLevel 0~6이 특정 타겟을 지칭함 

- 첫 부팅 시, RunLevel 5로 실행 

  => 첫 부팅 시 어떤 RunLevel로 실행할지를 지칭하는 파일(링크 = 바로가기 아이콘 name=default.target)

  => /etc/systemd/system/default.target

  ![1561536707846](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561536707846.png)

  - 해당 링크를 다른 타깃으로 변경

    - #ln-sf (심볼릭 링크를 만드는 것 )	/lib/systemd/system/multi-user.target(지칭되는 곳=/lib/systemd/system= 실제로 RunLevel이 있는 곳)   /etc/systemd/system/default.target (어디에 어떤 이름의 링크를 만들지)

    - #ln   -sf   /lib/systemd/system/multi-user.target   /etc/systemd/system/default.target 

      : 부팅 시, text 기반 

    - #ln   -sf   /lib/systemd/system/graphical.target   /etc/systemd/system/default.target 

      : 부팅 시, graphic 기반 

      

- 자동완성 

  - 파일이나 디렉토리의 이름의 일부만 입력한 후, Tab 키를 이용





## Window System의 메모장같은 Text Editor 사용하기 

- #gedit 엔터 빵 

  : Text를 입력하는 창이 빵

  - 해당 프로그램은 GNOME(그놈)이라는 윈도우 매니저를 이용하는 경우에만 사용이 가능하다.

  ![1561595912278](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561595912278.png)

  - Linux 내 한글 전환 : 윈도우 키 + 스페이스 

    *** 리눅스에서는 확장자의 의미가 없음 , 그저 하나의 파일 이름에 불과함

    *** startx : text 기반의 command에서 x윈도우를 동작시킬 수 있다.

## Text 기반의 Edit

- text 기반의 command에서는 gedit와 같은 그래픽 기반의 명령들을 수행할 수 없다. 
  - 터미널 모드인 경우, 전통적으로 vi라는 터미널 기반의 Edit를 사용한다.

- vi 명령어 사용 

  - 입력모드 : 데이터, 글자를 수정하거나 입력할 때

    - 입력모드로 진입하기 위해서는 a 또는 i 키를 사용한다.
      - i : 현재 커서 위치에서 입력모드로 진입
      - a : 현재 커서의 다음 위치에서 입력모드로 진입

  - EX모드 : 저장하거나 빠져나올 때 

    - 입력모드를 빠져나와 EX모드로 진입하기 위해서는 ESC키를 사용한다. ( esc 키를 누른다.(EX모드로 넘어가기)

      - shift키  + :(콜론) + w : 저장 후 EX모드에 계속 위치함

      - wq : 저장하고 끝내기

      - q! : 저장하지 않고 끝내기 

        

      - x 키 : 현재 커서가 위치한 곳의 한글자를 지움

      - dd 따당: 지우기를 원하는 행의 행 전체를 지움

      - ndd : 여러 줄 삭제 

        - 3dd : 현재 커서 라인에서 3 줄이 삭제

      - yy : 해당 라인 전체를 복사 

      - nyy  : 여러 줄 복사 

        - 3yy : 현재 커서 라인에서 3 줄이 복사 

      - !v : 현재 히스토리 중 v라는 명령어로 시작하는 명령어를 실행

      - p : 복사된 라인을 원하는 곳에 붙여넣기

## 마운트 

- 물리적인 저장장치 ( = 하드디스크, CD/DVD, USB )를 사용하기 위해서 특정한 위치(디렉토리)에 연결하는 과정

- 각각의 물리적인 저장장치는 각각의 이름이 따로 잇음 

  - CD/DVD에 대한 장치 이름 => /dev 안에 cdrom이라는 이름으로 잡혀있음 : cdrom이라는 장치 이름

- #cd /dev => 현재 사용하는 working directory가 /dev로 변경됨 

- ls -al cdr* : cdr이라는 이름으로 시작되는 눔들 다 listing 됨

  ![1561600058773](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561600058773.png)

  - 실제 장치의 이름은 /dev/src0
  - cdrom 은 symbolic link로 일종의 바로가기 이름

- /run/media/사용자(root)의 아이디/CD타이틀 : 현재 자동으로 마운트된 CD/DVD (cdrom)이 들어있음

  - /run/media/root : 이곳에 cdrom이 자동으로 위치함 

    ![1561601421113](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561601421113.png)

  

## U마운트

- 현재 자동으로 되어있는 마운트를 해제 

- 디렉토리와 해당 ISO 파일과의 연결을 끊는 것 

- umount /dev/cdrom(/dev/sr0)

  ![1561601640283](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561601640283.png)

- 마운트 포인트를 만들어서 수동으로 마운트 

  - 현재 위치는 반드시 /root

  - 특정 디렉토리 (마운트 포인트)가 필요함
    - mkdir mycdrom (mkdir 만들 디렉토리의 이름)
  - 디렉토리와 CD/DVD를 연결
    - mount -t iso9660 /dev/cdrom /root/mycdrom
    - mount [어떤 타입을 마운트(CD/DVD(=iso9660), USB 등등)]  [/dev/cdrom(cdrom장치에 대한 이름)원본]  [어디에 마운트할지]
    - 다시 마운트 해제 후, 폴더 지우기 
      - rm -rf mycdrom



## ISO 파일을 제작해서 mount

- iso 파일(.iso) : 국제 표준 기구(ISO)에서 제정한 광학 디스크 압축 파일

  						### In Linux  

  : genisoimage(iso 이미지 발생기)를 사용하여 iso 파일을 쉽게 만들 수 있다. iso 표준 형식의 압축파일을 만들 수 있다. 

  : 해당 프로그램이 시스템에 설치가 되어 있는지부터 확인 

   - rpm을 이용해서 해당 프로그램(package)가 설치되어 있는지를 확인 

   - RPM (RedHat Package Manager)

     - ##### rpm -qa genisoimag : 해당 프로그램이 시스템에 설치되어 있는지 확인  ->만약, 설치가 되어있지 않으면, 설치를 우선적으로 진행한다.

     - ##### genisoimage -r -J -o boot.iso /boot : 이 프로그램을 이용해서 /boot 디렉토리의 내용을 iso 파일로 압축



- boot.iso라는 이름으로 /boot 안의 모든 것을 압축

  ![1561602954963](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561602954963.png)

  

- mybootimage 디렉토리를 생성하여 boot.iso를 마운트 

  ![1561603169777](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561603169777.png)







## 필수적인 명령어

1. ls (list) : 파일과 디렉토리의 목록을 출력하기 위해 사용 
   - 일반적으로 사용하는 옵션은 -al을 많이 이용
2. cd (change directory) : working directory를 이동하기 위해서 사용
   - cd 명령에 인자를 주지 않으면, 현재 사용자의 home directory로 이동 
3. pwd (print working directory) : 현재 사용하고 있는 working directory 출력하기 위해 사용
4. rm (remove) : 파일이나 디렉토리를 지울 때 사용
   - 많이 사용하는 옵션은 -rf 
   - -r : 특정 디렉토리 내의 파일과 디렉토리를 재귀적으로 삭제할 때 
   - -f (force) : 강제적으로 삭제, 강제적으로 모두 날림
   -  rm -rf  /root/myiso
5. cp (copy) : 파일이나 디렉토리를 복사할 때 사용
   - cp 원본 복사본
   - cp aaa.txt bbb.txt
6. touch : 파일 크기가 0 인 파일(데이더가 없는)을 생성할 때 사용 
   - touch newfile
     - [현재 eorking directory에 newfile이라는 파일이 없는 경우] 파일 사이즈가 0인, 빈 파일을 생성
     - [현재 eorking directory에 newfile이라는 파일이 있는 경우] 해당 파일의 수정 날짜를 현재 날짜로 변경
7. mv (move) 
   1. 파일을 이동할 때 사용
   2. 파일이나 디렉토리의 이름을 변경할 때 사용 
      - mv aaa.txt bbb.txt
8. mkdir (make directory)
   - 새로운 디렉토리 생성 
   - mkdir 내가 만들 새로운 디렉토리
9. rmdir (remove directory) : 디렉토리를 삭제하기 위한 명령
   - 단, 디렉토리 안에 파일이나 다른 디렉토리가 없어야함
   - rmdir보다 rm을 사용하는 것을 추천함
10. cat (concatenate) : Text로 작성된 파일의 내용을 출력
    - cat 파일 : 파일의 내용을 출력
11. head, tail 
    - head : Text 파일의 상위 10줄
    - tail : Text 파일의 하위 10줄
12. more : 페이지를 넘어갈 때마다 Text 파일의 내용을 페이지 단위로 출력
    - more anaconda-ks.cfg
13. clear : Terminal을 깨끗이 비운다.



## 사용자와 그룹과 퍼미션

- Linux는 다중 사용자 시스템 

- 기본적으로 root라는 이름의 superuser가 존재한다. 

- 모든 사용자는 특정 그룹에 소속된다.

- Linux 시스템은 여러 사용자가 사용가는 하고, 모든 사용자는 /etc/paasswd 파일에 정의 되어 있다. 

  - cat /etc/passwd : 현재 시스템의 사용자에 대한 모든 정보가 :으로 구분되어 저장되어 있다.

  - Linux 시스템을 구동하기 위해 필요한 사용자들이 OS에 의해 자동 생성되어 존재한다.

    ```
    root:x:0:0:root:/root:/bin/bash
    ```

    - 사용자 이름 : 패스워드(보안 상, x로 표기) : 사용자 ID : 그룹 ID : 사용자 전체 이름 : 홈 디렉토리 : 기본 쉘(명령어 해석기)
    - : 으로 구분
    - 패스워드 : 보안 상, x로 표기
      - 각 사용자에 대한 패스워드는 /etc/shadow
      - cat /etc/shadow : 패스워드가 암호화되어 기록되어 있다.
    - 사용자 ID : 각각의 사용자마다 숫자가 부여됨, 같을 수 없음
    - 그룹 ID : 그룹마다 숫자가 부여됨 , /etc/group 에 저장된 그룹에 대한 정보 

  - root만 접근 가능

    - /etc/passwd : 사용자에 대한 정보 

    - /etc/shadow : 사용자 패스워드에 대한 정보 

    -  /etc/group : 어떤 그룹이 어떤 그룹 아이디를 가지고 있는 지 등 그룹에 대한 정보 

      - 사용자 생성 시, 사용자와 그룹의 이름을 함께 만들어준다.

      ```
      centos:x:1000:centos
      ```

      - 그룹 이름 : 	: 그룹ID 

- root라는 superuser만 새로운 사용자를 추가할 수 있다.

  - useradd testuser  : testuser라는 이름의 사용자를 추가
  - 특정 옵션 없이 사용자를 추가하면, 사용자 ID는 맨 마지막 사용자 ID +1 로 자동 부여됨, 또 사용자의 이름과 같은 그룹이 생성되고, 사용자는 해당 그룹에 포함된다.
  - useradd -u 1111 testuser: 추가할 사용자의 특정 사용자 ID를 직접 부여할 수 있다.
  - useradd -g root testuser : 추가할 사용자의 그룹을 root 그룹으로 추가 
  - useradd -d /newhome testuser : 기본적으로 일반 사용자의 홈 디렉토리는 /home/testuser로 설정된다. -d 옵션을 지정하면, testuser의 홈디렉토리를 /newhome으로 



1. #useradd -g centos testuser : centos 라는 그룹에 testuser를 추가한다.

![1561612806591](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561612806591.png)

2. 새로운 사용자는 추가 했지만, 비밀번호를 설정하지 않아 로그인을 할 수 없다. 

   - #passwd testuser

     ![1561612978273](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561612978273.png)

3. 사용자의 정보 수정 

   - #usermod -g root testuser	(testuser의 그룹을 root로 변경)

4. 사용자 삭제 

   - #userdel -r testuser

     - -r : 해당 사용자의 홈 디렉토리까지 같이 삭제 

       

## 파일과 디렉토리의 소유와 퍼미션



```
-rw-r--r--.  1 root root   1022  6월 27 19:29 sample.txt
```

1.  맨 앞 1칸 : 디렉토리 인지 파일인지 링크인지 

   - -: 파일
   - d: 디렉토리
   - l : 링크(심볼릭 링크)를 지칭

2. 나머지 9칸 : 해당 파일 또는 디렉토리의 퍼미션을 지칭

   - rw-							r--						r--

     420 = 6					400 = 4				400 = 4		=> 이 파일에 대한 퍼미션은 644

     소유자의 퍼미션	그룹의 퍼미션	기타/other 퍼미션

     1. 소유자인 root는 읽고, 수정할 수 있지만, 실행할 수는 없다.
     2. root 그룹의 사람은 file의 소유자는 아니지만, 그룹이 root이므로 읽을 수는 있고, 수정하거나 실행할 수 없다. 
     3. 소유자도 아니고, 소유자와 같은 그룹도 아닌 경우, 읽을 수만 있다. 만약, ---인 경우 접근자체 불가하다.

     

     - r/-	w/-	x/-

       readable	writavble	excutable

       읽을 수 있는	수정할 수 있는 	실행할 수 있는

3. -rw-r--r--.  1 root                                       root   1022  6월 27 19:29 sample.txt

   퍼미션				이 파일을 가지는 소유자	그룹

   

4. ```
   d 		r-x 	r-x 	---. 17 root root   4096  6월 27 20:36 .
   디렉토리 소유주	그룹	  소유자도 그룹도 아닌
   
   dr-xr-xr-x. 17 root root    224  6월 26 23:23 ..
   ```

- centos와 testuser는  other사용자 이므로  /root에 접근할 수 없다.

  ![1561616066116](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561616066116.png)

![1561615813928](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561615813928.png)

 - centos 라는 사용자의 그룹을 변경

   ![1561616002275](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561616002275.png)

- centos가 root 그룹으로 변경 되었기 때문에 r-x의 퍼미션을 갖게 된다. 

  ![1561616150546](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561616150546.png)

- -rw-r--r--.  1 root root   1022  6월 27 19:29 sample.txt     를 

  소유자와 같은 그룹의 사람만 해당 파일을 읽거나 수정이 가능항 상태로 만들고 실행은 안되게 맹글으

  ==> rw-	rw-	---

  ​		6		6		0

- 파일에 대한 퍼미션 변경 : chmod 660 sample.txt

  ![1561617658344](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561617658344.png)

- 파일에 대한 소유자 변경 : chown centos sample.txt (root의  sample.txt 파일을 centos에게 넘어감)

  ![1561617916282](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561617916282.png)

- 파일에 대한 소유자 변경 : chown centos.centos sample.txt (파일에 대한 소유자와 그룹을 동시에 변경 - 사용자와 그룹 모두 centos로 변경)

  ![1561618025737](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561618025737.png)

- 파일에 대한 그룹 변경 : chgrp centos sample.txt (해당 파일에 대한 그룹만 변경)

  ![1561617961474](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1561617961474.png)



## Linux의 파일 시스템

## = inode 기반 자료구조로 구성

: inode 객체는 해당 파일에 대한 퍼미션 정보를 가지고 있음, 실제 데이터는 데이터 블록이라는 disk 어딘가에 있으며, inode를 통해서 접근



- 심볼릭 링크 = 바로가기와 같음
  - link에 대한 inode가 만들어짐 . 원본 파일을 가리키는 inode.
  - 실제 데이터를 보기 위해서는 link의 inode를 통해 원본 파일에 접근하고, 원본 파일의 inode를 통해 실제 데이터제 접근한다. 























































