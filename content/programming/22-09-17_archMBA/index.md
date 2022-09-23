+++
title = "T2チップ搭載MacBookAirにArchLinuxをインストールする"
description = "意外とすんなり入ります"
date = 2022-09-17
[extra]
[taxonomies]
categories = ["blog"]
tags = ["ArchLinux","Apple","MacBookAir"]
+++

AppleT2セキュリティチップを搭載するMacBookAir9,1にArchLinuxをインストールしたので備忘録だにょ.

# Install

- [こ↑こ↓ (T2 Linux wiki)](https://wiki.t2linux.org/distributions/arch/installation/)に従って、どうぞ.
	- （T2用のカーネルであればdkmsによるモジュールの追加は必要）ないです.
	- __macOSは消さないでとっておいてください、お願いします！なんでもしますから！__(なんでもするとは言ってない）
	- ブートローダーはGRUBで、パパパっとやって終わり！

# CPUがｱﾂｩｲ!

- [こ↑こ↓](https://wiki.t2linux.org/guides/fan/)にあるmbpfanが使える.自分でビルドして、どうぞ.
	- AURにあるものはたぶん使えないってそれ一番言われてるから（

# あかん、これじゃwifiが死ぬぅ！

- [https://wiki.t2linux.org/guides/wifi-bluetooth/](https://wiki.t2linux.org/guides/wifi-bluetooth/)

	- どうやらmacOSからwifiとBluetoothのファームウェアをパクってくるらしい.

# オーディオが逝キスギィ
- [https://wiki.t2linux.org/guides/audio-config/](https://wiki.t2linux.org/guides/audio-config/) 

	- configファイルがありますねぇ！

	- MacBookAir9,1だけファイルの中身が微レ違.

# 暴れるなよ...暴れるなよ...（サスペンドできない）

- 丸2日悩んだ末、shellスクリプト書いて一発で直りました（たぶんここで躓いている人多い気がする。漏れだけか？）

- 以下のスクリプトを`/usr/lib/systemd/system-sleep`に保存してください.

```bash
#!/bin/sh

case $1 in
    pre)  modprobe -r brcmfmac ;;
    post) modprobe brcmfmac  ;;
esac

```

# おわりに
それなりに快適に動作しています.イヤホンとスピーカーの自動切り替えができないのと、サスペンド後にBluetoothが死ぬ（これはmacOSでもあったのでLinuxのせいでは
ない希ガス）のを我慢すれば実用上問題ないかと.　みんなもLinuxを使おうね！
