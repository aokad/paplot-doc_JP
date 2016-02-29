************************
install
************************

| paplotは次のマシンで動作します。
|

 * Linux系サーバ (HGCスパコン含), Linux ディストリビューション
 * MacOS X
 * Windows

| paplotを実行するにはpython 2.7 もしくはpython 3 が必要です。
| (python 2.6 は未検証)
|

 * :ref:`Linux系の場合 (HGCスパコン, cygwin含) <linux>`
 * :ref:`MacOS Xの場合 <linux>`
 * :ref:`Windowsの場合 <windows>`

.. _linux:

================================================
Linux系の場合 (HGCスパコン, cygwin含)
================================================

1. paplot のインストール
--------------------------

.. code-block:: bash

  cd {install したいディレクトリ}
  git clone https://github.com/Genomon-Project/paplot.git
  cd paplot

  python setup.py build install
  
  # 上のコマンドでエラーが出る場合
  export PATH=~/.local/bin/:$PATH
  python setup.py build install --user

| 正しくインストールされたか確認します。
|

.. code-block:: bash

  pa_plot conf
  **********************
     hello paplot !!!
  **********************

  (デフォルト設定値が表示される)

| このような表示が出れば成功です。
| 
| インストールが終わったら、:doc:`quick_start` をお試しください。
| 


================================================
MacOS Xの場合
================================================

1. ソースファイルのダウンロード
------------------------------------

| paplotのサイトからDownloadZIP ボタンを押して、zipファイルをダウンロードします。
|

https://github.com/Genomon-Project/paplot

| :command:`git` コマンドが使える方は :command:`git clone https://github.com/Genomon-Project/paplot.git` でもよいです。
|

2. paplot のインストール
--------------------------

| ターミナルを起動してダウンロードしたディレクトリに移動します。
| 
| ターミナル.appがDockの中にない場合、次からたどることができます。
| Finder → 「移動」メニュー → 「アプリケーション」を選択 → 「ユーティリティ」ディレクトリを開く → 「ターミナル」を起動
| 
| <user name>は自分のユーザ名です。
| :command:`whoami` コマンドを入力しても確認できます。
|

.. code-block:: bash

  cd {downloadしたディレクトリ}
  # 大抵は以下でOKです。
  # cd /Users/<user name>/Downloads/paplot-devel


| インストールします。
|

.. code-block:: bash
  
  python setup.py build install --user

3. PATHの設定
----------------

| このままではpa_plotがどこにあるかわからないので、インストールされているところにPATHを通します。
| 大抵、ここにあります。
|

:doc:`/Users/<user name>/Library/Python/2.7/bin`

| ここにない場合は :command:`find / -name pa_plot` とコマンドを入力してインストールされているところを探します。
|

.. code-block:: bash

  export PATH={installしたディレクトリ}:$PATH
  # 大抵は以下でOKです。
  # export PATH=/Users/<user name>/Library/Python/2.7/bin:$PATH


| 正しくインストールされたか確認します。
|

.. code-block:: bash

  pa_plot conf
  **********************
     hello paplot !!!
  **********************

  (デフォルト設定値が表示される)

| このような表示が出れば成功です。
|
| インストールが終わったら、:doc:`quick_start` をお試しください。
| 

4. 補足：PATH設定を忘れないようにする
---------------------------------------

| ↑で設定したPATHは再起動すると忘れてしまうので、
| 起動するたびに :command:`export PATH={installしたディレクトリ}:$PATH` コマンドを入力する必要があります。
| ここでは、起動しても自動的に再設定されるようにします。
|
| 設定ファイルを作成します。
|

.. code-block:: bash

  vi ~/.bash_profile

| ファイルが開いたら :command:`i` と入力して編集モードにします。
| ファイルにすでに何か記入されていたら、↓キーで最後の行に移動します。
| 
| <user name>は自分のユーザ名です。
|

.. code-block:: bash

  export PATH=/Users/<user name>/Library/Python/2.7/bin:$PATH

| 入力したら :command:`ESC` キーを押して、編集モードから抜けます。その後、 :command:`:wq` と入力して保存して終了します。
|

.. _windows:

====================================
Windows系の場合
====================================

1. Pythonのインストール
---------------------------

| winPython もしくはPython(x,y)をインストールするのが手軽だと思います。
| cygwinでも動きます。
| cygwinの場合は :ref:`Linux系の場合 (HGCスパコン, cygwin含) <linux>` を参照してください。
|

 * winPython http://winpython.github.io/
 * Python(x,y) http://python-xy.github.io/

| python 2.7.10 と python 3.5.1 は動作確認済みです。
| 

2. paplot のインストール
-----------------------------

| paplotのサイトからDownloadZIP ボタンを押して、zipファイルをダウンロードします。
| ダウンロードしたファイルは適当なフォルダに解凍します。
| 

https://github.com/Genomon-Project/paplot

| インストールしたフォルダにコマンドプロンプトがありますので、起動します。
| WinPython-64bit-3.5.1.2 を標準でインストールした場合、ここにあります。
| 
:doc:`C:\\Program Files\\WinPython-64bit-3.5.1.2\\WinPython Command Prompt.exe`

| 起動した画面に以下を入力します。
| 
.. code-block:: bash

  cd {zipを解凍したフォルダ}
  python setup.py build install


| Windowsの場合、 :command:`pa_plot` コマンドにパスが通っていないのでバッチファイルを使用します。
| zipを解凍したフォルダに :doc:`pa_plot.cmd` がありますので、ノートパッド等テキストエディタで開いて編集します。
| 
.. code-block:: bash

  set pa_plot="C:\Program Files\WinPython-64bit-3.5.1.2\python-3.5.1.amd64\Scripts\pa_plot"

| pa_plotの実際の場所を記入してください。
| 数字はインストールしたpythonのバージョンにより変化します。
| 
| 編集したバッチファイルをpythonコマンドプロンプトと同じフォルダにコピーします。
| 
| pythonコマンドプロンプトで、先ほど作成したバッチファイルを実行します。

.. code-block:: bash

  >pa_plot.cmd conf
  **********************
     hello paplot !!!
  **********************

  (デフォルト設定値が表示される)

| このような表示が出れば成功です。
| 
| **注意：Windows標準のコマンドプロンプトでは動作しません。**
| **必ずPythonのコマンドプロンプトを使用してください。**
| 
| 以降、 :command:`pa_plot` コマンドは :command:`pa_plot.cmd` と読み替えてください。
| 
| インストールが終わったら、:doc:`quick_start` をお試しください。
| 

