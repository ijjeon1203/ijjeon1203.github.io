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
기본적으로 지역을 한국으로 설정하시고 한국어로 언어를 설정하시면 /etc/apt/sources.list에 빨간색으로 http://kr.archive.ubuntu.com/ubuntu/로 나와있을겁니다.


문제 혹은 에러
간혹 아래 나와 있는 문제들처럼 설치할 수 없다고 오류가 뜰 때가 있는데 저장소에서 해당패키지에 대한 정보를 가지고 있지 않거나 일시적으로 서버가 작동하지 않을 수도 있다.

E: 아카이브를 받을 수 없습니다. 아마도 apt-get update를 실행해야 하거나 --fix-missing 옵션을 줘서 실행해야 할 것입니다.
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
위와 같은 상황일 때 apt-get의 패키지 서버를 다른 주소로 해서 다시 실행하면 제대로 설치되는 경우도 있다.



apt-get 서버 변경
http://kr.archive.ubuntu.com/ubuntu/ -> http://ftp.daumkakao.com/ubuntu/로 변경
파일 편집기 vim에서 파일(/etc/apt/sources.list)을 열고 아래와 같은 명령어로 문자열을 치환해줍니다.

:%s/kr.archive.ubuntu.com/ftp.daumkakao.com


동작 확인
apt-get를 통해서 제대로 동작하는지 확인

$ sudo apt-get update; sudo apt-get upgrade -y;


Ubuntu 소프트웨어 업데이트 서버를 daum으로 변경 (sources.list)


최초 Ubuntu 설치 시 Ubuntu SW 업데이트를 위한 서버가 kr.archive.ubuntu.com 으로 되어있다.


이 주소를 그대로 사용할 수도 있으나, 속도가 문제다.


나의 소중한 시간을 위하여 daum 서버 (daumkakao로 변경) 로 설정하도록 한다.



CTRL + ALT + T 를 입력하여 터미널을 실행한다.


vi를 통해 source.list 를 수정한다. (vi가 익숙하지 않다면 gedit 등의 다른 편집기를 사용해도 된다.)



관리자 권한으로 수정이 가능한 파일이기 때문에 sudo로 열어준다.



sudo vi /etc/apt/sources.list


":"를 눌러 명령어 입력모드로 가서 아래 키워드를 입력하여 찾아 바꾸기를 한다.



:%s/kr.archive.ubuntu.com/ftp.daumkakao.com



파일 내부에서 kr.archive.ubuntu.com 문자열을 ftp.daumkakao.com 으로 변경하는 명령이다.



":"를 눌러 wq를 입력하여 vi를 저장하고 종료한다.




sudo apt-get update를 해보면 daumkakao server를 통해 업데이트 되는 것을 볼 수 있
