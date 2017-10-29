====================================================================
Edisonへ書き込み出来ない [ write error: No space left on device ]
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



1. 初めに
-------------------------------------

Edisonを触っていると、急に動作がおかしくなる瞬間がある。

自分の事象が発覚したのは、gitでhttpにpullリクエストを送った際に、DNSの処理に失敗した点だ。

多分、他にもいろんな箇所で、[ write error: No space left on device ]に引っかかると思われる。

記事を書く前にIntelのフォーラムにて書き込みを行いましたが、良い結果が得られなかったので遅れて記事を書きます。

https://communities.intel.com/thread/55388?tstart=0


2. 症状
-------------------------------------

突然、Edisonのrootディレクトリが満杯になり、Edisonの設定がうまくいかない。

 write error: No space left on device

と言うエラーメッセージが出る。



- du -sh /var/log/journal/*

をするとデカい容量を持ったlogファイルがたくさん出てくる。



3. 原因
-------------------------------------

/var/log/journal/　より先のディレクトリに、Edison起動時のログが保存されており、

起動後とに次々にファイルを作っていきます。



4. 対策（緊急）
-------------------------------------

緊急の対策方法です。まずは一回試してください。

- rm  -r  /var/log/journal/*

このコマンドで、journalに保存されているlogを全部消します。

ただ、これだと再度、再起動をした際にはまたlogが作られてしまいます。

これを毎回繰り返すのもアレなので、次の暫定対策をおすすめします。

5. 対策（暫定）
-------------------------------------

journalのlogの設定を変更します。

- vi /etc/systemd/journald.conf


開いたら、以下の箇所に変更します。

　[Journal]

　#Storage=persistent

　Storage=volatile


これで、logは毎回取りますが、増えたりしないので、一先ず安心？かなぁ。

Storageの項目をpersistentからvolatileに変更しました。

フォーラムはあまりこの方法が好きではなさそうなので、自己判断でお願いします。




6. なぜ起きたのか
-------------------------------------


どうもね、Intelのエンジニアの方が、Edisonの終了時と起動時の情報を取得したかったそうで、

OS終了→log保存→OS起動→別名log保存→確認

と、するための機能なのかな。

英語がね・・・辛いのでね・・・


7. 今後について
-------------------------------------

一先ず、上の方法で自分は解決しましたが、今後FWのアップデートに織り込むかどうかは不明です。

当分、そのままで行くかもしれません。もしくは別の箇所に実はバグが・・・とかあるかも。

知らないうちに解決されているかもしれません。

今後もフォーラムのチェックを行っていきますが、どうなることやら・・・

https://communities.intel.com/thread/55388?tstart=0


あと、自分の解析手法もどこかでまとめたいなぁ～

ではでは。



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

:初版: 2014/10/28

:作成者: Yuta kitagami
:連絡先: kitagami@artifactnoise.com
:twitter: @nonNoise
