# linux ip 수동 설정방법

sudo nmcli connection modify "Wired connection 2" ipv4.addresses 192.168.1.29/24 ipv4.method manual
sudo nmcli connection up "Wired connection 2"

# 


nmcli connection show "Wired connection 1" | grep autoconnect

nmcli connection show "Wired connection 2" | grep autoconnect

nmcli connection show "Wired connection 3" | grep autoconnect



sudo nmcli connection modify "Wired connection 2" connection.autoconnect yes


30 기준으로 똑같이 설정하고 해결 됨

