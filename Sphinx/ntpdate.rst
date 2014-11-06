====================================================================
Edisonの時計合わせ
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



1. 初めに
------------------------------------- 

Edusinでの時計合わせの方法についてまとめます。

Edisonにはモジュールの内部にリアルタイムクロック(RTC)があったりするので、その機能を使ってみます。

また、Linuxではファイルの更新日を比較したりする仕組みも多いので、できるだけ早い段階で時間合わせをしておいた方が良い。

一度、時間合わせを行えば、電源さえ入っていれば時間は記憶されます。
が、一度電源を抜いてしまいますと、誤差が大きくなってしまう。
なので、Edisonにはバックアップ電池をつけるための端子があるようだ。（未検証）

今回は、手動で時計合わせをせず、せっかく無線LANに繋がるデバイスなので、NTPサーバーへアクセスしたいとおもいます。


2. コマンドで今の時間を見てみる
------------------------------------- 

Linuxには二種類のクロックがあり、

- システムクロック
	- Linuxのシステム上で動く時計であり、Linux上の時計は殆どシステムクロックを使う。定期的にハードウェアクロックから時間を読み出す。

- ハードウェアクロック
	- RTCなどを使い、ハードウェアレベルで時間を刻む。Linux上ではあまり使われないが、電源を切った後にもカウントするので、次回起動時に時計合わせが必要ない。

となっています。

ためしに、今のそれぞれの時間を確認しましょう。

- システムクロック
	- date
	- > 時間が表示される
- ハードウェアクロック
 	- hwclock
	- > 時間が表示される

初期の状態だと、dateには何か時間が表示されるかもしれません。が、hwclockの方は0:0:0:0のままだったような気がします。（記事を執筆中に更新してしまったので元に戻せないw）

一先ず、今の状況が分かれば、続いてNTPサーバーより時間合わせに移りたいと思います。

3. ntpdateをインストールする
------------------------------------- 

Linuxではよく、ntpdateが入っている事が殆どですが、Edisonにはまだntpdateが標準では入っていません。また、opkgにも無かったので、手動で入れていきます。


まずは、ntpdateのソースをダウンロードします。

- curl http://www.eecis.udel.edu/~ntp/ntp_spool/ntp4/ntp-4.2/ntp-4.2.6p5.tar.gz -o ntpdate.tar.gz
- tar zxvf ntpdate.tar.gz
- cd ntp-4.2.6p5/

続いて、コンフィグの設定を行います。

- ./configure --prefix=/usr --sysconfdir=/etc --enable-linuxcaps --with-binsubdir=sbin --with-lineeditlibs=readline

最後に、makeして、インストールします。

- make
- make install

無事にntpdateがインストールされたか確認してみます。

- ntpdate -v ntp.nict.jp

何か時間らしき物が見えれば成功です。


4. ntpdateを使って時計を合わせる
------------------------------------- 

さて、早速時計合わせをしていきます。

まず、今のEdisonの時計と、ネット側にあるNTPの時刻との差を見にいきます。

- ntpdate -q ntp.nict.jp

最後の行の「adjust time server 133.243.238.164 offset 0.026365 sec」が重要な箇所で、さらに最後の offset 0.026365 sec　が、設定時間の差です。

続いて、NTPの時刻に合わせてみましょう。

- ntpdate -bv ntp.nict.jp

このコマンドにより、Edison内のシステムクロックがNTPにより、世界標準時間(UTC)に合わさります。

続いて、世界標準時間では日本時間と差があるので、日本時間に設定します。所謂タイムゾーンを変えると言うことです。

- export TZ=JST-9

以上で、時間合わせの設定が終わりです。

試しに、

- date

で、今の正しい日本時間が表示されていれば正解です。

5. ntpdateで遊んでみる
------------------------------------- 

さて、せっかくntpdateを入れたのですから、そのコマンドを使って遊んでみましょう。

ますは、結局システムクロックとハードウェアクロックがあったけど、今どうなってるの？から。

- date
	- > 日本時間で表示
- hwclock
	- > 世界時間で表示

と、こういった形で時間が保存されます。　通常はこのままで問題ありません。無理やり合わせることも出来ますが、世界時間はたまに必要となるので、このままでいいでしょう。

次に、今のNTPサーバーとの時間差を知りたい時ですが、

- ntpdate -q ntp.nict.jp
	- > server 133.243.238.164, stratum 1, offset 0.043990, delay 0.05780
	- > server 133.243.238.243, stratum 1, offset 0.044843, delay 0.05847
	- > server 133.243.238.244, stratum 1, offset 0.044612, delay 0.05783
	- > server 133.243.238.163, stratum 1, offset 0.043710, delay 0.05836
	- >  7 Nov 01:11:08 ntpdate[11329]: adjust time server 133.243.238.164 offset 0.043990 sec

って感じになり、最後の[offset 0.043990 sec]が、時間差になります。


では、実験を一つしてみましょう。NTPで設定したEdisonを一旦シャットダウンし、電源を抜いた状態で数秒放置します。

- halt  

シャットダウンコマンドです。文字の流れが止まり、[  OK  ] Reached target Shutdown.  となれば、電源側のUSBケーブルを抜いてください。

んで、カップラーメンを食べるか、そのまま電源を抜いた状態で３分程度待ちましょう。

数分後、再び電源を入れ、Edisonへloginしてください。

そして、再び

- ntpdate -q ntp.nict.jp

どうでしょう。offsetの箇所の時間がものすごく増えた気がしません？w

そう、EdisonにはRTC用バックアップ電池が無いので、電源を抜くと電源を抜く前の時間で止まってしまいます。
なので、解決策としては、

- 起動時に毎回NTPサーバーへアクセスする
- RTC用のバックアップ電池を付ける
- リチウムポリマー電池等を付けて、Linuxを止めない仕組みを作る
- USBに接続しっ放しで、抜けたらNTPへ接続コマンドを手動で入れる

って所でしょうかね。一番簡単な方法はバックアップ電池を付けることなんですが、何を付ければいいのか資料が無いので、なるべくUSB抜かない方向でいきたいと思います。

後日バックアップ電池に関して追記予定





参考資料
--------------------------------

http://www.linuxfromscratch.org/blfs/view/svn/basicnet/ntp.html

http://webkaru.net/linux/ntpdate-command/

http://futuremix.org/2004/01/localtime

http://www.atmarkit.co.jp/ait/articles/0812/26/news120.html

提供
--------------------------------

ArtifactNoise.

.. image:: img/ANlogoMark02.png
	:alt: ArtifactNoise
	:scale: 40%
	:target: http://artifactnoise.com
	
管理情報
------------------------------------------------

:初版: 2014/11/07

:作成者: Yuta kitagami
:連絡先: kitagami@artifactnoise.com
:twitter: @nonNoise


