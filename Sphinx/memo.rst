====================================================================
Edisonのチョイテク
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



1. nano エディターを入れる。
------------------------------------- 

Edisonには vi しか入っていなかったので、vi弱な自分はnanoがどうしても欲しかった。
調べたら見つけたので残しておきます。

- wget http://www.nano-editor.org/dist/v2.2/nano-2.2.6.tar.gz && tar xvf nano-2.2.6.tar.gz && cd nano-2.2.6 && ./configure && make && make install


が！！　日本語化がされてない・・・　随時、挑戦していきます・・・汗w

参考）　https://communities.intel.com/thread/55602

2. Edisonのttyドライバに関して
------------------------------------- 

とりあえずttyで何が乗ってるか調べてみました。

- ttyGS0
	- Arduino型に変換した際のシリアルポート
- ttyMFD0
- ttyMFD1
- ttyMFD2
	- MFDと言うドライバらしい http://kernelnewbies.org/Linux_3.15-DriversArch#head-cbc97bbb5edf0993e6b63bccca043fda1b799d6a
- ttyPTI0
- ttyPTI1
	- 不明。どこかで出てきたら、また調べよう。

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


