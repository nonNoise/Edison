====================================================================
Edison　で　mraaライブラリを使ってみる
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

	
1.初めに
---------------------------

2. mraaに関して
-----------------------------------------

3. mraaライブラリのインストール
-----------------------------------------

4. mraaをC言語で扱う
-----------------------------------------

5. mraaライブラリをPythonで扱う
-----------------------------------------

6. mraaライブラリの説明
-----------------------------------------

**mraa_gpio_context mraa_gpio_init (int pin)**

GPIOで使用するピンをmraaのピン番号で設定する。
 
**mraa_gpio_context 	mraa_gpio_init_raw (int gpiopin) **

GPIOで使用するピンを設定する。
 
**mraa_result_t 	mraa_gpio_edge_mode (mraa_gpio_context dev, gpio_edge_t mode) **

入力ピンで割り込みを行う際の状態変化検出を行う際の方法を設定
 
** mraa_result_t 	mraa_gpio_isr (mraa_gpio_context dev, gpio_edge_t edge, void(*fptr)(void *), void *args) **

割り込みが発生した際に実効する関数を設定
 
** mraa_result_t 	mraa_gpio_isr_exit (mraa_gpio_context dev) **

割り込み終了で元の関数に戻る。
 
** mraa_result_t 	mraa_gpio_mode (mraa_gpio_context dev, gpio_mode_t mode) **

GPIOのモード設定
 
** mraa_result_t 	mraa_gpio_dir (mraa_gpio_context dev, gpio_dir_t dir) **

GPIOのモードを反映させます。
 
** mraa_result_t 	mraa_gpio_close (mraa_gpio_context dev) **

GPIOの使用を終了します。
 
** int 	mraa_gpio_read (mraa_gpio_context dev) **

GPIO入力ピンの状態を読み出します。
 
** mraa_result_t 	mraa_gpio_write (mraa_gpio_context dev, int value) **

GPIO出力ピンに書き出します。
 
** mraa_result_t 	mraa_gpio_owner (mraa_gpio_context dev, mraa_boolean_t owner) **

なんだろう。
 
** mraa_result_t 	mraa_gpio_use_mmaped (mraa_gpio_context dev, mraa_boolean_t mmap) **

GPIOのMAP関数（ちょい不明、CPUのレジスタにアクセス出来るかも？）

提供
--------------------------------

ArtifactNoise.

.. image:: img/ANlogoMark02.png
	:alt: ArtifactNoise
	:scale: 40%
	:target: http://artifactnoise.com
	
管理情報
------------------------------------------------

:初版: 2014/11/15

:作成者: Yuta kitagami
:連絡先: kitagami@artifactnoise.com
:twitter: @nonNoise

