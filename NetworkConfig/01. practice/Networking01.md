<h1>■Networking01</h1><br>
<h5>再配送の仕組みが理解できなかったため、実際にただ繋げるためだけのconfigを書きました。<br>図.01を見たらピンとくる方もいるはず。<br><br>

使用ソフト:GNS3<br>
※GNS3を使用するにはCisco IOSが必要なので、実機を買ってFTPでIOSを吸い出す(用途はバックアップ的な意味で・・・)<br>
自分はできるやつとできないやつがありました 2600や3600(うろ覚え)はできる 1812jはできない<br>
この理由がわかる方はご教示いただきたいです\(*'ω'*)/<br><br>

図.01<br>
<img src="https://raw.githubusercontent.com/sola-akiduki/networking_info/master/NetworkConfig/images/Networking01.PNG"><br>2年前に作成したものなので、config(コマンド等)がうまくいかなかった場合はすみません(/ω＼)<br>
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
