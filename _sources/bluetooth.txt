====================================================================
EdisonのBluetooth開発 
====================================================================

.. image:: img/intel.web.480.270.jpg
	:scale: 40%
	:target: http://www.intel.com/content/www/us/en/do-it-yourself/maker.html

.. image:: img/edison.png
	:scale: 40%

.. image:: img/Edison_top_view.png
	:scale: 30%
	:target: http://nonnoise.github.io/Edison/hardware.html

.. image:: img/edison02.jpg
	:scale: 30%


1. 早速試してみる。
------------------------------------- 


例えハードウェアがちゃんとしていても、LinuxでBluethoothを扱う以上、苦労するんだろうなと思っていたが、まさにそうだ。

まだEdisonに関して情報が少ないが（Edisonの告知サイトが多すぎて検索避けが出来ない！)、何とか開発出来そうなポイントまで辿り着いたのでメモを残しておきます。

まず、bluetoothを起動させます。（デフォルトでは起動していない。ひどいw）

- rfkill unblock bluetooth

.. note::
	
	rfkillってReFileKillかと思ったけど、RFKillで無線デバイスを管理するコマンドらしい。

	https://access.redhat.com/documentation/ja-JP/Red_Hat_Enterprise_Linux/6/html/Power_Management_Guide/RFKill.html
	
	紛らわしいなぁもう。

- bluetoothctl

このコマンドで、Bluetooth全般の管理が出来ます。便利便利。CUIでは[bluetooth]# と表示されるはずです。
終了する際は exit で終われます。

[bluetooth]# の状態から、

- power on 
- power off
- scan on

でbluetoothを探しに行ったり出来る見たい。

後は先人の方の記事を読めば行けそうw　

http://note.kurodigi.com/post-0-12/

最新のBT4.0がどう動くか分からないけど、先にBT2.0のSPPモードでも動かしてみたいと思います。
こうご期待。(2014/10/27)




参考サイト
------------------------------------------

https://communities.intel.com/thread/56270

https://access.redhat.com/documentation/ja-JP/Red_Hat_Enterprise_Linux/6/html/Power_Management_Guide/RFKill.html

http://note.kurodigi.com/post-0-12/


|

|

|





提供
--------------------------------

ArtifactNoise.

.. image:: img/ANlogoMark02.png
	:alt: ArtifactNoise
	:scale: 40%
	:target: http://artifactnoise.com
	
管理情報
------------------------------------------------

:初版: 2014/10/28

:作成者: Yuta kitagami
:連絡先: kitagami@artifactnoise.com
:twitter: @nonNoise

