<h1>■Networking01</h1><br>
<h5>再配送の仕組みが理解できなかったため、実際にただ繋げるためだけのconfigを書きました。<br>図.01を見たらピンとくる方もいるはず。<br><br>

使用ソフト:GNS3<br>
※GNS3を使用するにはCisco IOSが必要なので、実機を買ってFTPでIOSを吸い出す(用途はバックアップ的な意味で・・・)<br>
自分はできるやつとできないやつがありました 2600や3600(うろ覚え)はできる 1812jはできない<br>
この理由がわかる方はご教示いただきたいです\(*'ω'*)/対応機種じゃないって以外で何か仕組みが違うのでしょうか?<br><br>

図.01<br>
<img src="https://raw.githubusercontent.com/sola-akiduki/networking_info/master/NetworkConfig/images/Networking01.PNG"><br>config(コマンド等)がうまくいかなかった場合はすみません(/ω＼)<br>
「特権モード」からコピーしたコマンドを流していくイメージ<br><br>
●R1
```html
conf t
interface f0/0
ip address 172.16.0.1 255.255.255.0
no shutdown
exit
router ospf 10
network 172.16.0.0 0.0.0.255 area 0
```
●R2
```html
conf t
interface f0/0
ip address 172.16.0.10 255.255.255.0
no shutdown
interface f0/1
ip address 172.16.10.1 255.255.255.0
no shutdown
exit
router ospf 20
network 172.16.0.0 0.0.0.255 area 0
network 172.16.10.0 0.0.0.255 area 10
area 10 stub
```
●R3
```html
conf t
interface f0/1
ip address 172.16.10.2 255.255.255.0
no shutdown
exit
router ospf 30
network 172.16.10.0 0.0.0.255 area 10
area 10 stub
```
●R4
```html
conf t
interface f0/0
ip address 172.16.0.20 255.255.255.0
no shutdown
interface f0/1 
ip address 172.16.20.1 255.255.255.0
no shutdown
exit
router ospf 40
network 172.16.0.0 0.0.0.255 area 0
network 172.16.20.0 0.0.0.255 area 20
```
●R5
```html
conf t
interface f0/1
ip address 172.16.20.250 255.255.255.0
no shutdown
interface s0/0
ip address 192.168.20.250 255.255.255.0
no shutdown
exit
router ospf 50
network 172.16.20.0 0.0.0.255 area 20
redistribute rip metric 100 subnets
router rip
network 192.168.20.0
redistribute ospf 50 metric 10
version 2
```
●R6
```html
conf t
interface f0/0
ip address 172.16.0.30 255.255.255.0
no shutdown
interface f0/1
ip address 172.16.30.1 255.255.255.0
no shutdown
exit
router ospf 60
network 172.16.0.0 0.0.0.255 area 0
network 172.16.30.0 0.0.0.255 area 30
area 30 nssa

※オプション(RIPとEIGRP間で疎通できるようになるとメモにありました)
area 30 nssa default-information-originate
```
●R7
```html
conf t
interface f0/1
ip address 172.16.30.2 255.255.255.0
no shutdown
exit
router ospf 70
network 172.16.30.0 0.0.0.255 area 30
area 30 nssa
```
●R8
```html
conf t
interface f0/1
ip address 172.16.30.250 255.255.255.0
no shutdown
interface s0/0
ip address 10.1.30.250 255.255.255.0
no shutdown
router ospf 80
network 172.16.30.0 0.0.0.255 area 30
redistribute eigrp 10 subnets
area 30 nssa
router eigrp 10
network 10.1.30.0 0.0.0.255
redistribute ospf 80 metric 100000 10 255 1 1500
```
●R9
```html
conf t
interface f0/0
ip address 10.1.20.1 255.255.255.0
no shutdown
interface s0/0
ip address 10.1.30.1 255.255.255.0
no shutdown
exit
router eigrp 10
network 10.1.20.0 0.0.0.255
network 10.1.30.0 0.0.0.255
```
●R10
```html
conf t
interface f0/1
ip address 192.168.10.1 255.255.255.0
no shutdown
interface s0/0
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
router rip
network 192.168.10.0
network 192.168.20.0
version 2
```
●R11
```html
conf t
interface f0/0
ip address 10.1.20.2 255.255.255.0
no shutdown
exit
router eigrp 10
network 10.1.20.0 0.0.0.255
```
●R12
```html
conf t
interface f0/1
ip address 192.168.10.2 255.255.255.0
no shutdown
exit
router rip
network 192.168.10.0
version 2
```

</h5><h3>■まとめ</h3><h5><p>
再配送は動きがわかりづらい(わからない)というのが自分の感想<br>
あと、実際に使用されてるのかも聞きたいです('ω')<br>
業務でしか学べないこともたくさんあるのでネットワーク業務やりたいのですが・・・<br>
なかなか希望の職種にはつけないみたいです・・・<br>
今はネットワークチームの設計書も見ることができないので悲しいです



