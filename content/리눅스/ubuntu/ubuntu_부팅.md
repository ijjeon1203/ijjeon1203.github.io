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
