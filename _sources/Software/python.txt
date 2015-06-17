====================================================================
EdisonにPython環境を構築する
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


1. EdisonにPython環境を構築する
-------------------------------------
(1) Pythonが起動することを確認する

	- python

※終了するときは exit() で終われます。

(2) pipをインストールする

	- curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

	- python get-pip.py

	- pip

※もしここでエラーが出たらTwitterでご報告ください。>@nonNoise


(3) pipを使って色々入れてみる


	- pip install flask
	- pip install pyserial
	- pip install sphinx
	- pip install virtualenvwrapper

などなどw

(4) うまく行かないライブラリもありました。

	- pip install ipython

		- インストールまでうまく行ったけどコマンドを実行するとエラーが出る。(海外ユーザーでも議論されている

	うまく行かなかった物があれば、随時、ご報告お待ちしております>@nonNoise


(5) お馴染み "Hello World!"

	- python

	>> print("Hello World!")

	Hello World!


お疲れさまでした。
後は、お好きなようにPythonで遊べるでしょうw

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
