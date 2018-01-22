# VirtualBox Troubleshooting log
* 2017-04-27. magicpotato
* 버추얼박스 세팅법 - https://forums.virtualbox.org/viewtopic.php?f=1&t=49066

> 왠만하면 버추얼박스 쓰지 말자. 노답임.

1. VBoxNetNAT.exe 도 방화벽 OUT에 등록해 줘야 한다.
  vboxheadless.exe도 방화벽 OUT에 등록해줘야 한다. exe는 그냥 다 등록하자.
  
2. NAT의 경우 게이트워이가 .2, dns가 .3이다. dhcp는 15부터 증가
네트워크 카드 순서에 따라서 10.0.2.x의 중간 숫자가 올라간다.
STATIC세팅을 하고 ip addr flush dev eth0 을 해줘야 한다.

3. NAT Network의 경우 GUI상으로 추가하면 제대로 작동하지 않으므로
커맨드라인으로 192.168.15.0 네트워크로 추가해 줘야 한다.
게이트웨이는 .1 이다. dns는 없고, dhcp는 15부터 증가.
이 경우 dns가 없으므로 168.126.63.1을 지정해 주면 된다.
port forwarding으로 호스트PC의 포트를 받아서 VPC로 연결이 되는데,
putty등으로 vpc에 접속할 수가 없다.
여기까지 적어놓고 보니 dhcp 사용하고 vpc당 포트포워팅 설정하는게 편한듯 --;
static으로 해서 잘되는건 착각이다.

4. 호스트전용 네트워크는 allow-hotplug enp0s8 같은식으로 시작하자. auto는 안먹는듯.
   이거 ip로 핑 쏴봤자 응답이 없으므로 바로 putty로 테스트 해볼것.
   우분투로 putty접속 실패시 14-1-교환 순으로 변경하자.
   
중간중간 뭔가 반영이 잘 안되면 vpc를 리부팅 하는게 낫다.

**결론 : 부팅한채로 lshw로 장비인식 시키니 즉빵, 되도록이면 auto, dhcp를 이용하면 인식이 잘된다. 켜자마자 작동하는건 잘 안되는 듯.**

아래 방식은 해결책이 아니다.
```
m@/etc/init$ cat vbox_network_warm.conf
start on startup
lshw -short
```

1. DHCPCLIENT에 의해 resolv.conf 가 제대로 생성되도록 세팅

```
sudo vi /etc/dhcp/dhclient.conf`
prepend domain-name-servers 10.0.2.3; 로 수정할 것.
```
 
2. 캐시 싹 날리고 깔끔하게 재시작

```
RTNETLINK answers: File exists
ip addr flush dev eth0  ===> 이걸 하면 ip는 제대로 잡히고 ping도 잘 나간다.
/etc/init.d/networking restart
```

현재 부팅이후 매번 restart 하는 방법밖에 모르겠다 (버추얼박스 기준)
