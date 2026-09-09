우분투 16.04 /var/lib/dpkg/lock 잠금 파일을 얻을 수 없습니다 해결방법

- reboot 로 해결


sudo apt-get upgrade
- ㅅㅂ 버전 안맞을때 취소방법?
  - 맥 OS X 에서 타임머신이 좋음

---
PPA를 포함하지 않은 간소화한 유틸 설치는 민트 리눅스 항목을 참고하십시오.

http://optic.tistory.com/47

아래 내용을 터미널(ctrl+alt+t)에서 복사/붙여넣기 하십시오.

sudo apt update && sudo apt install -y chromium-browser chromium-browser-l10n gstreamer1.0-fluendo-mp3 gstreamer1.0-libav gstreamer1.0-packagekit gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly frei0r-plugins libmatroska6v5 unrar gdebi lame x265 clamtk ufw ffmpeg faad giflib-tools wavpack opus-tools p7zip p7zip-full p7zip-rar ppa-purge partitionmanager clamav libclamunrar7 pinball kpat kblocks kbreakout kmahjongg kmines kreversi gwenview autoconf automake git pitivi ghostscript fonts-noto-cjk fonts-noto-cjk-extra guake kolourpaint gnome-weather pdfshuffler redshift-gtk calibre audacity default-jre

sudo ufw enable

sudo add-apt-repository -y ppa:rvm/smplayer

sudo add-apt-repository -y ppa:videolan/master-daily

sudo add-apt-repository -y ppa:libreoffice/ppa

sudo add-apt-repository -y ppa:ozmartian/apps

sudo add-apt-repository -y ppa:linrunner/tlp

sudo add-apt-repository -y "deb http://archive.canonical.com/ubuntu `lsb_release -cs` partner"

sudo add-apt-repository -y ppa:qbittorrent-team/qbittorrent-stable

sudo add-apt-repository -y ppa:mc3man/mpv-tests

sudo add-apt-repository -y ppa:lazka/ppa

sudo add-apt-repository -y ppa:recoll-backports/recoll-1.15-on

sudo add-apt-repository -y ppa:apandada1/brightness-controller

sudo add-apt-repository ppa:kritalime/ppa

sudo add-apt-repository ppa:starws-box/deadbeef-player

sudo add-apt-repository ppa:lucioc/sayonara

sudo add-apt-repository ppa:team-xbmc/ppa

sudo add-apt-repository ppa:ubuntu-x-swat/updates

sudo apt update ; sudo apt full-upgrade -y ; sudo apt install -y smplayer vlc libreoffice libreoffice-l10n vidcutter tlp adobe-flashplugin qbittorrent mpv quodlibet recoll brightness-controller krita deadbeef sayonara kodi

wget -q -O - http://archive.getdeb.net/getdeb-archive.key | sudo apt-key add -

sudo sh -c 'echo "deb http://archive.getdeb.net/ubuntu $(lsb_release -sc)-getdeb apps" >> /etc/apt/sources.list.d/getdeb.list'

sudo apt update && sudo apt install -y calibre

sudo apt autoremove ; sudo tlp start

sudo apt install -y --install-recommends linux-generic-hwe-18.04 xserver-xorg-hwe-18.04

sudo ubuntu-drivers autoinstall

reboot

* guake 터미널은 f12키를 누르면 내려오고 한번 더 f12하면 올라갑니다. f11키 누르면 최대화 되었다가 한번 더 f11하면 원래크기로 복원됩니다. 폰트 설정은 noto sans cjk kr 으로 선택하십시오. 어도비 플래시 ppa 적용. pinta에서 kolourpaint로 변경. 음악재생기는 쿼드리벳+데드비프+사요나라로 변경함. deluge에서 큐빗토런트로 변경함.

<Lxqt 설치>

sudo apt update ; sudo apt install lxqt-*

reboot

한컴오피스 뷰어 : http://www.hancom.com/cs_center/csDownload.do

한글입력을 위해 fcitx를 따로 설치하고자 하신다면 아래와 같이 실행해주십시오. (기본적으로 fcitx가 설치되어있음)

sudo apt install fcitx fcitx-hangul fcitx-config-gtk

sudo im-config    (fcitx을 선택합니다.)

exit



우분투 마테 : sudo apt install mate-tweak

우분투 : sudo apt install gnome-tweak-tool dconf-editor

그놈 소프트웨어 센터 : sudo apt install gnome-software



필요에 따른 유틸 설치 (우분투/민트/데비안) : http://optic.tistory.com/22



엔비디아 그래픽 드라이버 설치

sudo add-apt-repository ppa:graphics-drivers/ppa

sudo ubuntu-drivers autoinstall

sudo nvidia-xconfig

sudo reboot

(재부팅 후)

sudo nvidia-settings

* 지포스 6~7 시리즈는 진하게 표시한 부분을 nvidia-304 로, 지포스 8~9 시리즈는 nvidia-340 으로 변경하십시오.

본인의 그래픽 사양은 lspci | grep VGA 으로 확인하실 수 있습니다.



AMD 그래픽 드라이버 설치

sudo apt install xserver-xorg-video-amdgpu



HP 리눅스 프린팅 및 이미징 시스템 (HPLIP)

sudo apt install hplip-gui



<for intel cpu> sudo apt install  intel-microcode

<for amd cpu> sudo apt install amd64-microcode

<업데이트> sudo apt update && sudo apt full-upgrade -y



* root 계정의 암호 생성 : sudo passwd root



Linux Mint : http://optic.tistory.com/47

Ubuntu : http://optic.tistory.com/145

Ubuntu MATE : http://optic.tistory.com/115

Lubuntu : http://optic.tistory.com/146

Xubuntu : http://optic.tistory.com/147

Kubuntu : http://optic.tistory.com/144

KDE neon : http://optic.tistory.com/269

Ubuntu Budgie : http://optic.tistory.com/233

리눅스에서 하드디스크 파티션 설정 예제 : http://optic.tistory.com/112

민트 & 우분투 PPA : http://optic.tistory.com/58

우분투 18.04 for 라즈베리파이 (Raspberry Pi) : http://optic.tistory.com/41

우분투, 민트에서 터미널을 통해 비발디 또는 오페라 브라우저를 설치하는 방법 : http://optic.tistory.com/9

rufus : http://optic.tistory.com/80

unetbootin : http://optic.tistory.com/33

터미널을 이용하여 clamav를 활용하기 : http://optic.tistory.com/265

암호관리 유틸 키패스 : http://optic.tistory.com/116

snap : http://optic.tistory.com/118

구글 크롬 & 크로미엄의 즐겨찾기를 백업하고 복구하기 : http://optic.tistory.com/142

큐빗토런트에서 ip필터목록을 적용시키기 : http://optic.tistory.com/63

deluge에서 차단목록 사용하기 : http://wp.me/p67C5e-1m

파이어폭스 플래시 플래이어 수동 설치 : http://optic.tistory.com/271

크로미엄 펩퍼플래시 : http://wp.me/p67C5e-1T

etcher를 이용하여 usb에 리눅스 이미지 굽기 : http://wp.me/p67C5e-1t

크롬/크로미엄에서 플래시 사용설정 : http://optic.tistory.com/256

샌드박스와 비슷한 firejail : http://wp.me/p67C5e-2v

네이버 웨일 브라우저 : http://optic.tistory.com/140

https://www.virtualbox.org/wiki/Linux_Downloads



출처: https://optic.tistory.com/119 []




원인 파악: Shutter는 스크린샷 편집을 위해 GooCanvas라는 라이브러리를 사용합니다. 하지만 특정 Ubuntu 버전부터 이 라이브러리가 기본 패키지 목록에서 빠지게 되었고, 이로 인해 Shutter 설치는 되지만 "편집" 버튼은 먹통이 된 상태입니다.

의존성 수동 해결 (1단계 & 2단계): * libgoocanvas-common: 공통 리소스 파일 설치.

libgoocanvas3: 실제 동작에 필요한 라이브러리 바이너리.

libgoo-canvas-perl: Shutter(Perl 기반 프로그램)와 라이브러리를 연결해 주는 브릿지 역할.

유추: 이 3가지 파일을 순서대로 설치해야만 Shutter가 편집 모드로 진입할 수 있는 "다리"가 놓이게 됩니다.

프로세스 초기화 (3단계): sudo killall -9 shutter 명령어를 통해 백그라운드에서 돌고 있는 Shutter 설정을 완전히 강제 종료합니다. 단순히 창을 닫는 것만으로는 새로 설치한 라이브러리가 적용되지 않기 때문입니다.

기능 활성화 확인 (4단계): 재실행 시 Shutter는 시스템에 설치된 libgoo-canvas-perl을 인식하게 되고, 비로소 회색으로 죽어있던 [Edit] 버튼이 활성화됩니다.

최신 PPA 버전은 위에서 언급하신 libgoocanvas 문제를 내부적으로 해결하여 배포되므로 별도의 수동 다운로드가 필요 없습니다.


sudo apt-get install shutter

기본적으로 패키지를 설치한 후 Shutter를 실행하면 편집(Edit) 버튼이 비활성화되는 문제가 있습니다.

아래 파일을 다운로드합니다.

https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas-common_1.0.0-1_all.deb

아래 파일도 다운로드 후 설치
https://launchpad.net/ubuntu/+archive/primary/+files/libgoocanvas3_1.0.0-1_amd64.deb

https://launchpad.net/ubuntu/+archive/primary/+files/libgoo-canvas-perl_0.06-2ubuntu3_amd64.deb

sudo killall -9 shutter

Shutter 재실행

Shutter를 다시 실행하면 캡처 후 Edit 버튼이 활성화됩니다.

sudo add-apt-repository ppa:linuxuprising/shutter
sudo apt update
sudo apt install shutter