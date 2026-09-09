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
