====================================================================
Edison初期化方法（工場出荷時及び最新版FW)
====================================================================

.. image:: ../img/intel.web.480.270.jpg
	:scale: 40%
	:target: http://www.intel.com/content/www/us/en/do-it-yourself/maker.html

.. image:: ../img/Edison11.JPG
	:scale: 50%

.. image:: ../img/EA05.JPG
	:scale: 30%

.. image:: ../img/Edison_top_view.png
	:scale: 30%



1.Edisonを初期化出来る環境
--------------------------------------------

Edisonの初期化は結構難しい。RasPiならSDカードを交換すれば良いのだが、EdisonはオンボードのフラッシュROMなので、
外部から書き換えを行う必要があります。

Intel社から紹介されている方法は、LinuxとWindowsのみに対応しており、Macに関しては随時行うそうです。

Edisonの初期化は、本当に全部初期化にしますので、各設定類はすべて削除されます。

例えば、僕見たいにパスワードを忘れたり間違えたりして、どうにもならなくなった際に使って見てください。

あと、最新版のFWにするには、この方法が一番です。逆に、古いFWに戻したくてもROMがどこにあるのか探すのも一苦労汗w

2.初期化ファイルのダウンロード
--------------------------------------------

https://communities.intel.com/docs/DOC-23242 より、「　Edison Yocto complete 　」
をダウンロードしてください。

ダウンロードしたら、zipファイルなので解答してください。

解答したら、コマンドプロントで解答したフォルダーまで移動します。

3. 初期化の手順
--------------------------------------------

(1) EdisonをPCに接続します

(2-1) Linux上から書き換えを実行

	.. warning::

	自分のUnintu環境では、dfu-utilが無かった為、 「apt-get install dfu-util」を行った後に実行しました。

	- sudo ./flashall.sh

(2-2) Winsowsの場合（Intel非純正のサピート方法です。）

	以下のリンクより、dfu-util.exeをダウンロード。
	https://dl.dropboxusercontent.com/u/54378433/dfu-util/dfu-util.exe

	ダウンロードしたdfu-util.exeを、解答したedison-image-ww36-14ファイルに移動します。

	cdコマンドを使い、edison-image-ww36-14ファイルまでコマンドで移動します。

	移動先で、
		- flashall
	を実行すると、数秒間の待ち状態になります。

	参考資料： https://communities.intel.com/message/256593

(3) Edisonの電源側を抜いて、差し直す。（なるべくFTDI側は残しておいた方がいいです。完了時が分かりますので)

(4) コマンドが流れて行って、１０秒近くたったら、自動的に再起動します。

(5) edison login: が表示されたが完了。


参考資料
--------------------------------

http://www.adafruit.com/datasheets/EdisonUserGuide.pdf

|

|

|


提供
--------------------------------

ArtifactNoise.

.. image:: ../img/ANlogoMark02.png
	:alt: ArtifactNoise
	:scale: 40%
	:target: http://artifactnoise.com


管理情報
------------------------------------------------

:初版: 2014/10/25

:作成者: Yuta kitagami
:連絡先: kitagami@artifactnoise.com
:twitter: @nonNoise
