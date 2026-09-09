
nmcli
- 리눅스에서 NetworkManager를 커맨드라인으로 제어하는 도구
- GUI 없이 네트워크 연결(Wi-Fi, 이더넷, VPN 등)을 설정하고 관리


```
# 전체 네트워크 상태 확인
nmcli general status

# 연결된 장치 목록
nmcli device status

# Wi-Fi 목록 스캔
nmcli device wifi list

# Wi-Fi 연결
nmcli device wifi connect "SSID이름" password "비밀번호"

# 현재 연결 목록 확인
nmcli connection show

# 특정 연결 활성화/비활성화
nmcli connection up "연결이름"
nmcli connection down "연결이름"

# IP 정보 확인
nmcli device show eth0

# 고정 IP 설정 (예시)
nmcli connection modify "연결이름" ipv4.addresses 192.168.1.100/24
nmcli connection modify "연결이름" ipv4.gateway 192.168.1.1
nmcli connection modify "연결이름" ipv4.dns 8.8.8.8
nmcli connection modify "연결이름" ipv4.method manual
nmcli connection up "연결이름"
```