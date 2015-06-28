====================================================================
★EdisonにPython環境を構築する
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


 EdisonにPython環境を構築する
--------------------------------------------------------------------------


Edisonでは、すでにPythonが標準に入っておりますが、通常のPCと同じように非常にパワフルに動作しますので、Python関連のライブラリを強化します。


1) Pythonが起動することを確認する

	- python

	※終了するときは exit() を入力して 終了します。


2) pipをインストールする

	pipはPythonのライブラリをインストールするためのコマンドです。

	Edisonのopkgにはpipが無いため、Pythonソースを使ってインストールを行います。

	インストール用のソースをダウンロードします。

	- curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

	ダウンロードしたソースをPythonで実行します。

	- python get-pip.py

	インストール完了です。試しにpipとコマンドを入力してみてください。

	- pip

	※もしここでエラーが出たらTwitterでご報告ください。>@nonNoise


3) pipを使ってPythonを強化してみる

	★ Webサーバー用マイクロフレームワーク Flask

	- pip install flask

	★ ドキュメント作成支援ライブラリ Sphinx

	- pip install sphinx

	★ 画像処理用イメージライブラリー Pilliow (PIL)

	- pip install pillow

	★ デーモン管理用ライブラリ supervisor

	- pip install supervisor

	★ シリアル制御用ライブラリ PySerial

	- pip install pyserial


	などなどw


5) せっかくなので、お馴染み "Hello World!"

	コマンドでpythonを入力し、エンター

	- python

	>>の先に以下のソースを入力してエンター

	- >> print("Hello World!")

	Hello World!

	Pythonはスクリプト言語なので開発が非常にシンプルで賢いのでおすすめです。


お疲れさまでした。

後は、お好きなようにPythonで遊んでみてください。

|

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
