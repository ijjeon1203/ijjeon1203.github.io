ctrl alt delete
- 잠금

vm 입력후 tab키 두번 누르기 

붙여넣기 
shift + insert 
shift ctrl +v 

# 명령어 

ipa 명령어

보드 버전 확인 명령어 
do apt-cache show nvidia-l4t-co

rm -rf [삭제할_폴더_경로]

linux
여러 문장한번에?

dmesg 

- dmesg -c 
 - 이후 한번더하면 수정사항만 확인 가능 

makefile 그냥 make 만 하면 댐 

lsmod

vi /etc/systemd/digitron.sh

uname

uname -a

uname -r 

sshfs root@192.168.1.179:/usr/src /mnt/nvd1

bitbake fsl-image-gui


# linux 명령어 중 
설치중 y , n , a : accept  

---
dmesg 명령어 
- 커널 디버깅 명령어 
- 여기서 찾을 수 있음 


# linux 명령어 
ls -r /dev | grep dma 

- r 은 recursive 

정상동작시 /dev/ 안에 뜨는지 확인

todo 
- test
- apllication 만드는방법 
 - tools 확인 


/dev/xdma0_ ~~~ 
- device file

tools 빌드 에러 
%d 대신 %ld long double 

reg_rw 는?

----------------------------------
cat /proc/devices | grep xdma

# make 파일 명령어 
sudo insmod xdma.ko poll_mode=1

ls /dev/xdma*

make clean

ls -R /dev | grep dma

# 메이크 사용법 

config_bar_num=1 xvc_bar_num=2 make  

CONFIG_NV_VIDEO_IMX390=y
- y 는 built in 
 드라이브 항상 오름 
- m 은 module 

CONFIG_SND_HDA_INTEL=m
- 모니터 출력시 필요 옵션
- 원래 snd 는 사운드 드라이버
- 있으면 동작안함

CONFIG_USB_OTG=y
- 꺼야 잘돌아감
- 나중에 안정화 되면 쓸수도 있음 
 - 근데 usb 있으니 굳이 할필요 없음

CONFIG_MICREL_PHY=m

rgmii 인터페이스 

gmi 
- gigabit 
- reduce 
- mii : multimedia in..~~~~

micrel사의 phy  사용한다 

# 리눅스

tmp 에 넣으면 재부팅하면 사라짐 

```
$ user 
# root
~ 틸다 
```

home 빼고는 전부 root권한 
sshfs 를 마운트 해서 merge 

---


# 명령어 옵션


기본으로 debug 모드로 빌드됨 사이즈가 큼 
debuging 심볼 다 삭제 
strip 디버깅 심볼 삭제 



## 서비스 설정

## 서비스 시작

```
sudo systemctl daemon-reload
sudo systemctl enable digitron.service
sudo systemctl status digitron.service
```

sudo systemctl status digitron.service 
- 이후 ctrl c 로 닫기?
- 서비스 실행 확인 명령어

sudo systemctl status digitron.service
- 확인 코드

```



리눅스 창(terminal) 마다 기억하는게 다를까 

su
- 관리자 권한으로 로그인 


터미널 키는 명령어 



sudo du -sm *
du (Disk Usage)

파일 / 디렉터리의 실제 디스크 사용량을 계산

ls -lh와 달리 디스크 블록 기준 사용량을 보여줌

3️⃣ -s (summary)

하위 디렉터리 상세 내역을 출력하지 않고

각 인자(*)에 대해 요약 결과만 출력

4️⃣ -m (megabytes)

결과를 MB 단위로 표시
결과를 MB 단위로 표시

1 = 1MB

5️⃣ *

현재 디렉터리의 모든 파일과 디렉터리

쉘에서 먼저 확장됨 (globbing)

현재 디렉터리의 모든 파일과 디렉터리

쉘에서 먼저 확장됨 (globbing)

