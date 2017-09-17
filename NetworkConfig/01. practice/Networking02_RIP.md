<h1>■Networking02</h2><br>
<h5>Networking02ではRIPのみで繋いだ時のconfigを書きました。<br>
version1、version2、1と2の混合とか行っていきます。<br><br>

■RIPの概要<br>
#################################<br>
(ここに概要などを記載する)<br>
v1とv2の違いとか<br>
クラスフルとかクラスレスとかVLSMとか<br>
#################################<br>

■図.2-1 \<RIP version1\><br>
<img src="https://raw.githubusercontent.com/sola-akiduki/networking_info/master/NetworkConfig/images/Networking02_RIP_v1.PNG"><br><br>
●R1
```html
configure terminal
interface f0/0
ip address 172.16.0.10 255.255.255.0
no shutdown
exit
router rip
network 172.16.0.0
```
●R2
```html
configure terminal
interface f0/1
ip address 172.16.0.20 255.255.255.0
no shutdown
interface f0/0
ip address 172.16.1.30 255.255.255.0
no shutdown
exit
router rip
network 172.16.0.0
```
●R3
```html
configure terminal
interface f0/0
ip address 172.16.1.40 255.255.255.0
no shutdown
interface f0/1
ip address 172.16.2.50 255.255.255.0
no shutdown
exit
router rip
network 172.16.0.0
```
●R4
```html
configure terminal
interface f0/0
ip address 172.16.2.60 255.255.255.0
no shutdown
interface f0/1
ip address 172.16.3.70 255.255.255.0
no shutdown
exit
router rip
network 172.16.0.0
```
●R5
```html
configure terminal
interface f0/0
ip address 172.16.3.80 255.255.255.0
no shutdown
exit
router rip
network 172.16.0.0
```
■図.2-2 \<RIP version1\><br>
<img src="https://raw.githubusercontent.com/sola-akiduki/networking_info/master/NetworkConfig/images/Networking02_RIP_v2.PNG"><br><br>


