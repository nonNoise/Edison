====================================================================
Edison開発方法（最新FWバージョン）
====================================================================

.. image:: img/intel.web.480.270.jpg
	:scale: 40%
	:target: http://www.intel.com/content/www/us/en/do-it-yourself/maker.html

.. image:: img/edison.png
	:scale: 40%

.. image:: img/edison02.jpg
	:scale: 30%

	
1.初めに
---------------------------

Edisonを買ってすぐのバージョンと、最新のファームウェアに書き換えた時とでコマンドやバグが変わってたので書き直しました。

ちなみに、今回試したFWは、
edison-weekly_build_68_2014-09-08_13-49-07
です。

cat /etc/version　で確認できます。


最新版のFWにする方法は、http://nonnoise.github.io/Edison/init.html　で説明しています。


2. Edisonを触ってみる
-----------------------------------------

loginまで無事に到着した方は、これからコマンドで進んでいきますので、マウスから両手を離してキーボードに集中してください。

それでは行きますよw

(1) login: の箇所に root と打ち込みエンター　（初期状態ではrootのパスワードは無い)

(2) login出来ました？試しにifconfigで何かが見えればOK

(3) 早速、Edisonの初期設定をしていきます。まずEdisonのWiFiを使ってインターネットにつなげます。

(4) コマンド[configure_edison --setup]を入力します。

- Configure Edison: Device Name
	- デバイスの名前を決めます。僕はedison-01　にしました。

- Configure Edison: Device Password
	- デバイスのパスワード(root共通)を設定します。ここを設定すると次回のログイン時に必要です。8～64文字で設定する必要があります。

- Configure Edison: WiFi Connection
	- WiFiを設定します。数秒後に自動的にスキャンしたリストを見せてくれますが、部屋のWiFiが見当たらない際は０再更新、１手入力を選択してください。

.. note::
	
	WiFiの設定で失敗、もしくは時間がかかる際は、Edisonをルーターの近くに持っていったり、金属系から遠ざけるなり行ってください。
	意外とアンテナ弱いです。もしかするとどこかの設定で強く出来るかも？


(5) WiFIの設定がうまく行ったかの確認をするために [ifconfig]を入力して、wlan0 にIPアドレスがあれば正解。


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


