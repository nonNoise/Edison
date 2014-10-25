====================================================================
Edison開発方法
====================================================================



.. image:: img/intel.web.480.270.jpg
	:scale: 40%
	:target: http://www.intel.com/content/www/us/en/do-it-yourself/maker.html

.. image:: img/edison.png
	:scale: 40%

.. image:: img/edison02.jpg
	:scale: 30%

	
nonNoise考案　Edison開発方法
--------------------------------------

.. toctree::
	:maxdepth: 1

	index
	python
	init

|

|


1.まずEdisonを買う。
---------------------------

Intel社から三種類、Edisonが発売されています。

一つはモジュール単品
http://akizukidenshi.com/catalog/g/gM-08569/

そしてブレークアウト基板付きセット
http://akizukidenshi.com/catalog/g/gM-08570/

最後に、Arduino変換基板付きセット
http://akizukidenshi.com/catalog/g/gM-08571/


値段的、サイズ的に扱いやすいブレークアウト基板付きセットを本サイトで紹介します。

他のセットについては、互換があったり無かったり、触れた機会に調査したいと思いますw


2. 開発環境を整える
-----------------------------------------

さて、ブレークアウト基板セット
http://akizukidenshi.com/catalog/g/gM-08570/
を買って、他にも色々必要です。

開発には、USB-MicroBが２本、２本ですよ？　２本必要ですw

１本は電源用、もう１本は通信用です。

電源用を接続するとPC上ではディスクとして見えます。
基板にLEDが付いたら電源用のUSBコネクタです。

通信用に接続すると、PC上ではFTDIのドライバのインストールが
開始されます。基板上のLEDは点灯しません。

どうやら、Edisonの電源ラインと通信用ラインは完全に独立していて、
先に通信側を接続して、COMポートを開くとEdisonの起動時の処理が見えたりします。
これ結構、便利でうれしい。さすがだねw

開発環境としてはこれだけ。

必要な物

◇ Edison Breakout Board : x1 : http://akizukidenshi.com/catalog/g/gM-08570/

◇ USB-MicroB : x2 : http://akizukidenshi.com/catalog/g/gC-07607/

◇ 保存ケース : x1 : http://akizukidenshi.com/catalog/g/gP-07327/

だけで一先ず十分です。


3. Edisonを起動してみる
-----------------------------------------

さて、早速起動してみますか。開封の儀は写真だけなのですっ飛ばします。

あ、ちなみにコネクタでマウントした後に小さなスペーサーが残るけど、それちゃんと付けておいた方が安心だよ
結構コネクタ壊れやすいから、ちゃんと付けておいた方が良いw

さて、もうYou!USBさしちゃうなYo!　ってことで、何も考えずにUSBポートに接続してください。

得に順番は関係ありませんが、僕は先にFTDIのチップが乗っている方を接続します。

(1) FTDIチップが乗っている方を先に接続
(2) COMポートが決まったらTeraTarm(Win)やscreen(Mac,Linux)でシリアル通信を行う準備をする。
(3) シリアル通信の速度は115200bpsです。それだけ設定してください。その他はデフォルトでOK
(4) シリアル通信の準備が出来たら、電源側のUSBを接続し、基板にLEDが灯ることを確認してください。
(5) 数秒後、Boot画面がずらずら出てくるはずなので、何も押さずに少し待つ。
(6) 電源さしてLEDも付いたのに文字が出ない際は、USBがちゃんと刺さっているか確認して(3)の速度を見直してください。
(7) login: と言う表記になれば起動成功！　おめでとうございます！　そしてようこそEdisonの世界へw

4. Edisonを触ってみる
-----------------------------------------

loginまで無事に到着した方は、これからコマンドで進んでいきますので、マウスから両手を離してキーボードに集中してください。

それでは行きますよw

.. warning::

	Edisonのシリアルターミナルでバグが一ヶ所あります。少し時間が立つと、最初の一文字を認識してくれません。
	ちゃんと文字が打たれているか確認ののち、最初の一文字が入っていない際は削除して再度打ち込んでください。
	多分、割り込みがうまく行ってないんじゃないかな・・・汗w




(1) login: の箇所に root と打ち込みエンター　（初期状態ではrootのパスワードは無い)

(2) login出来ました？試しにlsコマンドでopkg.binが見えればOK　（これが何か不明w）

(3) 早速、Edisonの初期設定をしていきます。まずEdisonのWiFiを使ってインターネットにつなげます。

(4) コマンド[ configure_edison ]を入力します。



	- Configure Edison: Device Name
		- デバイスの名前を決めます。僕はedison-01　にしました。

	- Configure Edison: Device Password
		- デバイスのパスワード(root共通)を設定します。ここを設定すると次回のログイン時に必要です。

	- Configure Edison: WiFi Connection
		- WiFiを設定します。数秒後に自動的にスキャンしたリストを見せてくれますが、部屋のWiFiが見当たらない際は０再更新、１手入力を選択してください。

.. note::
	
	WiFiの設定で失敗、もしくは時間がかかる際は、Edisonをルーターの近くに持っていったり、金属系から遠ざけるなり行ってください。
	意外とアンテナ弱いです。もしかするとどこかの設定で強く出来るかも？


(5) WiFIの設定がうまく行ったかの確認をするために [ifconfig]を入力して、wlan0 にIPアドレスがあれば正解。

.. warning::

	Wifiの設定が、何故か電源を落とした後に初期化されてしまいました。閣下はお怒りですw。対策を探しています。


5. Edisonを最新にする
-----------------------------------------

さて、何とかWiFiに接続できて、これからだってその前に、念のため色々と最新にしたいとおもいます。


(1) opkg　と言うパッケージマネージャのリストを更新します。 以下のコマンドを叩いてください。


	- ベースとなるライブラリリストファイル
		- curl http://nonnoise.github.io/Edison/_sources/Edison/base-feeds.conf -o base-feeds.conf

	- Intelが推奨するIoTライブラリリストファイル
		- curl http://nonnoise.github.io/Edison/_sources/Edison/intel-iotdk.conf -o intel-iotdk.conf

	- mraaと言うEdisonのIO回りを制御するためのライブラリリストファイル
		- curl http://nonnoise.github.io/Edison/_sources/Edison/mraa-upm.conf -o mraa-upm.conf

※この箇所は我流です。好き勝手に開発するにはこの辺を入れておいた方がおもしろい。

(2) ダウンロードしたコンフィグファイルを移動します。

	- cp base-feeds.conf /etc/opkg/
	- cp intel-iotdk.conf /etc/opkg/
	- cp mraa-upm.conf /etc/opkg/
	

(3) opkgを更新してパッケージを最新のものにします。

	- opkg update
	- opkg upgrade

(4) 試しにgitを入れてみましょう

	- opkg install git

これだけ。問題なく行ったら、

	- git

でgitコマンドが起動したら成功w












|

|

|

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

:初版: 2014/10/25

:作成者: Yuta kitagami
:連絡先: kitagami@artifactnoise.com
:twitter: @nonNoise

