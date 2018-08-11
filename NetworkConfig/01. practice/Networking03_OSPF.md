<h1>■Networking03</h2><br>
<h5>Networking03ではOSPFのみで繋いだ時のconfigを書きました。<br>
シングルエリア、マルチエリア、バーチャルリンクとか行っていきます。<br><br>

■OSPFの概要<br>
#################################<br>
(ここに概要などを記載する)<br>
シングルエリアとかマルチエリアとか<br>
バーチャルリンクとかHelloとか<br>
#################################<br>

・シングルエリア
●R1
```html
configure terminal
interface f0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
router ospf 10
network 192.168.1.0 0.0.0.255 area 0
```
●R2
```html
conf t
interface f0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
interface f0/1
ip address 192.168.1.2 255.255.255.0
no shutdown
exit
router ospf 20
network 192.168.1.0 0.0.0.255 area 0
network 192.168.2.0 0.0.0.255 area 0
```
●R3
```html
conf t
interface f0/0
ip address 192.168.3.1 255.255.255.0
no shutdown
interface f0/1
ip address 192.168.2.2 255.255.255.0
no shutdown
exit
router ospf 30
network 192.168.2.0 0.0.0.255 area 0
network 192.168.3.0 0.0.0.255 area 0
```
●R4
```html
conf t
interface f0/1
ip address 192.168.3.2 255.255.255.0
no shutdown
exit
router ospf 40
network 192.168.3.0 0.0.0.255 area 0
```
