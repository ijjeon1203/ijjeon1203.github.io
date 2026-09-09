# Ubuntu

# 정의

우분투 LTS 의미 및 차이점 우분투에서 LTS는 Long Term Support의 약자입니다. 오랜 시간 동안 지원을 받을 수 있다고 해석할 수 있는데요. LTS가 붙은 버전은 출시일로 부터 최대 5년 까지 꾸준한 기능 및 보안 업데이트를 지원합니다


# 종류



usb

우분투에서 인식하니까 폴더가 또하나있네 ㅇㅇ

ImportError: No module named 'tkinter'

- sudo apt-get install python3-tk

Linux(Ubuntu)에서 apt-get 패키지를 다운로드하는 서버를 변경

sources.list
파일 경로 및 열기
파일은 /etc/apt/에 위치

```
$ cd /etc/apt/
$ vim sources.list

```

기본 설정
기본적으로 지역을 한국으로 설정하시고 한국어로 언어를 설정하시면 /etc/apt/sources.list에 빨간색으로 [http://kr.archive.ubuntu.com/ubuntu/로](http://kr.archive.ubuntu.com/ubuntu/%EB%A1%9C) 나와있을겁니다.

문제 혹은 에러
간혹 아래 나와 있는 문제들처럼 설치할 수 없다고 오류가 뜰 때가 있는데 저장소에서 해당패키지에 대한 정보를 가지고 있지 않거나 일시적으로 서버가 작동하지 않을 수도 있다.

E: 아카이브를 받을 수 없습니다. 아마도 apt-get update를 실행해야 하거나 --fix-missing 옵션을 줘서 실행해야 할 것입니다.
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
위와 같은 상황일 때 apt-get의 패키지 서버를 다른 주소로 해서 다시 실행하면 제대로 설치되는 경우도 있다.

apt-get 서버 변경
[http://kr.archive.ubuntu.com/ubuntu/](http://kr.archive.ubuntu.com/ubuntu/) -> [http://ftp.daumkakao.com/ubuntu/로](http://ftp.daumkakao.com/ubuntu/%EB%A1%9C) 변경
파일 편집기 vim에서 파일(/etc/apt/sources.list)을 열고 아래와 같은 명령어로 문자열을 치환해줍니다.

:%s/kr.archive.ubuntu.com/ftp.daumkakao.com

동작 확인
apt-get를 통해서 제대로 동작하는지 확인

$ sudo apt-get update; sudo apt-get upgrade -y;

Ubuntu 소프트웨어 업데이트 서버를 daum으로 변경 (sources.list)

최초 Ubuntu 설치 시 Ubuntu SW 업데이트를 위한 서버가 [kr.archive.ubuntu.com](http://kr.archive.ubuntu.com/) 으로 되어있다.

이 주소를 그대로 사용할 수도 있으나, 속도가 문제다.

나의 소중한 시간을 위하여 daum 서버 (daumkakao로 변경) 로 설정하도록 한다.

CTRL + ALT + T 를 입력하여 터미널을 실행한다.

vi를 통해 source.list 를 수정한다. (vi가 익숙하지 않다면 gedit 등의 다른 편집기를 사용해도 된다.)

관리자 권한으로 수정이 가능한 파일이기 때문에 sudo로 열어준다.

sudo vi /etc/apt/sources.list

":"를 눌러 명령어 입력모드로 가서 아래 키워드를 입력하여 찾아 바꾸기를 한다.

:%s/kr.archive.ubuntu.com/ftp.daumkakao.com

파일 내부에서 [kr.archive.ubuntu.com](http://kr.archive.ubuntu.com/) 문자열을 [ftp.daumkakao.com](http://ftp.daumkakao.com/) 으로 변경하는 명령이다.

":"를 눌러 wq를 입력하여 vi를 저장하고 종료한다.

sudo apt-get update를 해보면 daumkakao server를 통해 업데이트 되는 것을 볼 수 있

# 설치

우분투 16.04 /var/lib/dpkg/lock 잠금 파일을 얻을 수 없습니다 해결방법

- reboot 로 해결

sudo apt-get upgrade

- ㅅㅂ 버전 안맞을때 취소방법?
    - 맥 OS X 에서 타임머신이 좋음

# 부팅

# 부팅 에러

원인

현상

해결

- fsck /dev/sda1
- sda는 오류창에 명시되있음

다른해결

우선 root 패스워드를 넣으면 single mode 로 들어갑니다. 여기서 fsck 를 이용해서 파티션들을 치료해주시고 재부팅하시면 됩니다. 만일 ext3를 쓰신다면...

fsck -f ext3 -y /dev/sda2
fsck -f ext3 -y /dev/sda3
fsck -f ext3 -y /dev/sdb1

# 설정

#계정

원격 들어갈 계정과 다름

원격으로 들어간것

- 한글 입력안됨
    - 텍스트 입력창이란 항목이 없음

## 비밀번호 설정

ubuntu 비밀번호 변경

sudo passwd

## ubuntu 동영상

Error
unknown file extension .mp4 matplotlib

## ubuntu 파일복사

- 복사중이면 꺼지면 안되지?

# 에러 1

np로 저장하기 전에 취소했으니 저장 안된것?

# 한글설정

ibus

# 설치

$ sudo add-apt-repository ppa:createsc/3beol
$ sudo apt-get update

$ sudo apt-get install ibus ibus-hangul

# 설정

Step 1
'System Settings' → Language Support → 진입초기에 install을 요구할 경우 진행한다.

'Language for menus and windows'에서 아래로 스크롤 해보면 한국어가 보일 것이다. 만약 없다면, Install/Remove Languages 를 선택하여 한국어 혹은 Korean을 선택한다.

Step 2
Text entry.

'System Settings' → Text Entry → 좌측 하단의 '+' 버튼 → Korean (Hangul) (IBus) 선택하여 추가

# 한글입력에러

ibus 실행
text entry  에서 설정후 해결

원격에서 text entry 가 없음

fcitx

- 이용할수 없음 뜨고 안됨

# 원격

sudo apt-get install xrdp
sudo apt-get install xfce4

/etc/xrdp/startwm.sh 파일 수정

./etc/X1/Xession -> ./usr/bin/startxfce4 로 변경

- 실행안됨
- startfxce4로만 바꾸니 실행가능

```
service xrdp restart

```

로 xrdp 서비스 재실행

- sudo로 실행하기

포트 변경 하고 싶으면 /etc/xrdp/xrdp.ini 파일로 port 부분을 원하는 포트변경

xfce4

- 추가로 원격 데스트탑 환경 지원

왜 Tab key를 잘못 인식하는지 이유는 알 수 없지만 "동일 프로그램 간의 전환"은 잘 쓰지도 않는 기능이므로 해당 단축키를 삭제하면 간단히 해결 된다. (많이 사용하는 기능은 "여러 프로그램 간의 전환"으로 <Alt key + Tab key> 조합이다.)
xfconf-query -c xfce4-keyboard-shortcuts -p /xfwm4/custom/'<'Super'>'Tab -r 명령어나

application - settings- windowsManager
창매니저 동일한 어플리케이션 창전환 switch windwo for same application 삭제로 해결

# 본체 종료

다꺼짐
원격에서도 sudo로 reboot 하면 다꺼짐

서버

Ubuntu server

파일시스템이 디렉토리
계층 구조와 연결되지 않으면 사용자가 해당 파일 시스템에 접근할수 없다
ㅍ
마운트

- 파일시스템을 디렉토리 계층구조의 특정 디렉터리와 연결하는 것을 말함

마운트 포인트
디렉토리 계층구조ㄴ에서 파일시스템이 연결되는 디렉토리

LVM
logical volume manager 파티션을 효율적으로 사용할수 있도록 해주는 관ㄹ디도구

- 파티션의 용량이 부족할 때 다른 파티션으로 연장하여 사용할 수있 다.
- 독립적으로 구성된 디스크 파티션을 하나로 연결하여 한 파티션 처람 사용할 수 있도록 해줌
PV physical volume 실제 하드디스크의 파티션
VG volume group 여러 개의 PV를 그룹으로 묶은 것
LV logical volume VG를 다시 적절한 크기의 파티션으로 나눌 때 각 파티션을 LV라함
PE physical extent PV가 가진 일정한 블록
LE logical extent LV가 가진 일정한 블록

LVM 생성 과정
기존 파일 시스템의 종류 변경

pv 생성
vg생성

vg 활성화
LV 생성
LV에 파일 시스텡 생성
LV 마운트

# 디스크 관리

파일 시스템 별 사용량 확인하기
파일 시스템 사용량을 이해하기 쉬운 단위로 표시하기
파일 시스
ㅔㅁ의 종류 정보 출력하기
리렉터리나 사용자별 디스크 사용량 확인하기

# 부팅

바이오스 단계
부트 로더 단계
커널 초기화 단계
init 실행 단계
로그인 프롬프트 출력

# 데몬프로세스

리눅스의 백그라운드에서 동작하면서 특정한 서비스를 제공하는 프로세스를 의미

- 웹서버 데이터 베이스 서버
원격 접속서버 등 각종 서비스를 제공하는 프로세스들

## 동작방식

독자형 standalone
혼자 스스로 동작하는 데몬
수퍼데몬에 의해 동작하는 방식
서비스 요청이 오면 수퍼 데몬이 해당 데몬 동작

- 자원을 아낄 수 있음

## 수퍼 데몽

유닉스에서 inetd -> xinetd 우분투에서

# 활용

단축키
Ubuntu에서는 예전 윈도우용과  스크린샷키가 동일하게 적용된다.

전체 화면 캡쳐 :Print Screen
윈도우창 화면 캡쳐 : Alt + Print Screen

스크린샷
또한 스크린샷 프로그램이 기본적으로 제공되는데, 위에 간단하게 소개드린 단축키를 사용해도 결국 "스크린샷" 프로그램으로 실행된다.

프로그램을 직접 실행하면 몇 가지 이점이 있다.

"다음 시간이 지난 후에 찍기" : 시스템 메뉴가 활성화된 상태에서는 단축키를 통한 캡쳐가 되지 않는다.
5초 뒤에 찍기로 설정 하고 잽싸게 시스템 메뉴를 누르고 기다리면 화면 캡쳐가 가능하다.
"잡을 영역선택" : 원하는 일부 영역만 선택하여 화면 캡쳐할 수 있다.

출처: [https://www.morenice.kr/108](https://www.morenice.kr/108) [morenice's blog]

ubuntu shutter 프로그램 사용법

sudo apt-get install shutter

다음처럼 세가지 패키지를 설치한 후 Shutter를 재시작해주면 편집 버튼이 활성화 됩니다.

( [https://itsfoss.com/shutter-edit-button-disabled/](https://itsfoss.com/shutter-edit-button-disabled/) )

1. 다음 링크에 있는 패키지를 다운로드한 후

[https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas-common_1.0.0-1_all.deb](https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas-common_1.0.0-1_all.deb)

더블 클릭하면 다음처럼 설치 화면이 보입니다.   설치 버튼을 클릭하여 설치를 합니다.

1. 다음 두 개의 링크에 있는 파일도 다운로드 후, 더블클릭하여 설치를 진행합니다.

[https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas3_1.0.0-1_amd64.deb](https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas3_1.0.0-1_amd64.deb)

[https://launchpad.net/ubuntu/+archive/primary/+files/libgoo-canvas-perl_0.06-2ubuntu3_amd64.deb](https://launchpad.net/ubuntu/+archive/primary/+files/libgoo-canvas-perl_0.06-2ubuntu3_amd64.deb)

3.이제  Shutter를 강제 종료합니다.

sudo killall -9 shutter

1. 다시 실행하여 캡처해보면 편집 버튼이 활성화 되어 있습니다.



sysstat는 sa 파일을 통해 로그를 남긴다.
해당 파일은 리눅스의 vi명령어를 통해 읽으면 깨짐

sa파일 열기 명령어
- 명령어

sar -f [파일명]
- 샘플
sar -f sa18








터미널창 두개에서 각각 bcompare시키면 탭추가하고 닫을때는 다같이 꺼지누 
