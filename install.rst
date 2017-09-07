************************
インストール
************************

| paplot は次のマシンで動作します。

 * Linux 系サーバ (HGC スパコン含)、Linux ディストリビューション
 * MacOS X
 * Windows

| paplot を実行するには python 2.7 もしくは python 3.5 が必要です。
| ( python 2.6 は未検証)

 * :ref:`Linux 系の場合 (HGC スパコン、cygwin 含) <linux>`
 * :ref:`MacOS X の場合 <macosx>`
 * :ref:`Windows の場合 <windows>`

.. _linux:

================================================
Linux 系の場合 (cygwin 含)
================================================

1. paplot のインストール
--------------------------

| paplot のサイトから最新版の ``Source code (zip)`` をダウンロードします。
| https://github.com/Genomon-Project/paplot/releases/

.. code-block:: bash

  cd {インストールしたいディレクトリ}
  # v0.5.4 の場合
  wget https://github.com/Genomon-Project/paplot/archive/v0.5.4.zip
  unzip v0.5.4.zip
  cd paplot-0.5.4/

  python setup.py build install
  
  # 上のコマンドでエラーが出る場合
  export PATH=~/.local/bin/:$PATH
  export LD_LIBRARY_PATH=~/.local/lib/:$LD_LIBRARY_PATH
  python setup.py build install --user

| 正しくインストールされたか確認します。

.. code-block:: bash

  paplot --version
  paplot-0.5.4


| このような表示が出れば成功です。
| 
| インストールが終わったら、:doc:`quick_start` をお試しください。

.. note::
  
  PATH 設定を忘れないようにする
  
  | ↑で export 設定した PATH と LD_LIBRARY_PATH はログアウトすると忘れてしまいます。
  | 再ログイン時に再設定されるよう設定ファイルに記入しておくことをお勧めします。
  | ``~/.bashrc`` もしくは ``~/.bash_profile`` ファイルに次の 2 行を記入してください。

  .. code-block:: bash
  
    export PATH=~/.local/bin/:$PATH
    export LD_LIBRARY_PATH=~/.local/lib/:$LD_LIBRARY_PATH
  

.. _macosx:

================================================
MacOS X の場合
================================================

1. ソースファイルのダウンロード
------------------------------------

| paplot のサイトから最新版の ``Source code (zip)`` をダウンロードします。

https://github.com/Genomon-Project/paplot/releases/

| ``git`` コマンドが使える方は ``git clone -b master https://github.com/Genomon-Project/paplot.git`` でもよいです。

2. paplot のインストール
--------------------------

| ターミナルを起動してダウンロードしたディレクトリに移動します。
| 
| 「ターミナル.app」が Dock の中にない場合、次からたどることができます。
| Finder → 「移動」メニュー → 「アプリケーション」を選択 → 「ユーティリティ」ディレクトリを開く → 「ターミナル」を起動
| 
| <user name>は自分のユーザ名です。
| ``whoami`` コマンドで確認できます。

.. code-block:: bash

  cd {ダウンロードしたディレクトリ}
  # 大抵は以下にあります
  # cd /Users/<user name>/Downloads/paplot-<version>


| インストールします。

.. code-block:: bash
  
  python setup.py build install --user

3. PATH の設定
----------------

| このままではターミナルは paplot がどこにあるかわからないので、インストールされている場所を PATH という環境変数に設定します。
| 大抵、ここにあります。

``/Users/<user name>/Library/Python/2.7/bin``

.. note::

  | ここにない場合は ``find / -name paplot`` とコマンドを入力してインストールされているところを探します。
  |
  | 4つ見つかるはずです。
  | このうち、ダウンロードしたディレクトリは使用しません。

  .. code-block:: bash
    
    {インストールしたディレクトリ}/bin/paplot               <--- ココです
    {インストールしたディレクトリ}/lib/python2.7/site-packages/paplot-0.2.6devel-py2.7.egg/EGG-INFO/scripts/paplot
    {ダウンロードしたディレクトリ}/paplot-devel/paplot
    {ダウンロードしたディレクトリ}/paplot-devel/build/scripts-2.7/paplot
  

.. code-block:: bash

  export PATH={インストールしたディレクトリ}/bin:$PATH
  export LD_LIBRARY_PATH={インストールしたディレクトリ}/lib:$LD_LIBRARY_PATH
  
  # 大抵は以下でOKです。
  # <user name>は自分のユーザ名に置き換えてください。
  # export PATH=/Users/<user name>/Library/Python/2.7/bin:$PATH
  # export LD_LIBRARY_PATH=/Users/<user name>/Library/Python/2.7/lib:$LD_LIBRARY_PATH


| 正しくインストールされたか確認します。

.. code-block:: bash

  paplot --version
  paplot-0.5.4

| このような表示が出れば成功です。
|
| インストールが終わったら、:doc:`quick_start` をお試しください。

.. note::
  
  PATH 設定を忘れないようにする
  
  | ↑で設定したPATHは再起動すると忘れてしまうので、
  | 起動するたびに ``export PATH=...`` コマンドを入力する必要があります。
  | ここでは、自動的に再設定されるようにします。
  |
  | 設定ファイルを作成します。
  
  .. code-block:: bash
  
    vi ~/.bash_profile
  
  | ファイルが開いたら ``i`` と入力して編集モードにします。
  | ファイルにすでに何か記入されていたら ``↓`` キーで最後の行に移動します。
  | 
  | <user name>は自分のユーザ名です。
  
  .. code-block:: bash
  
    export PATH=/Users/<user name>/Library/Python/2.7/bin:$PATH
    export LD_LIBRARY_PATH=/Users/<user name>/Library/Python/2.7/lib:$LD_LIBRARY_PATH
  
  | PATHの設定で入力したものと同じパスを入力してください。
  | 入力したら ``ESC`` キーを押して、編集モードから抜けます。その後、``:wq`` と入力して保存して終了します。

.. _windows:

====================================
Windows 系の場合
====================================

1. Python のインストール
---------------------------

| Windows の場合、標準では python はインストールされていませんので、まず python をインストールします。
| 標準 python でも paplot は動きますが、今後 python を使用してデータ解析される予定でしたら、数値計算系パッケージがあらかじめ用意されている winPython もしくは Python(x,y) をインストールすることをお勧めします。
| cygwin でも動きます。
| cygwin の場合は :ref:`Linux 系の場合 (HGC スパコン、cygwin 含) <linux>` を参照してください。

 * python (標準) https://www.python.org/
 * winPython http://winpython.github.io/
 * Python(x,y) http://python-xy.github.io/

| python 2.7.10、python 3.5.3 で動作確認済みです。
| 

2. paplot のインストール
-----------------------------

| paplot のサイトから最新版の ``Source code (zip)`` をダウンロードします。
| ダウンロードしたファイルは適当なフォルダに解凍します。

https://github.com/Genomon-Project/paplot/releases/

| Windows 標準のコマンドプロンプトを起動し、ダウンロードした zip ファイルを解凍したフォルダに移動します。

.. code-block:: bash

  cd {zip ファイルを解凍したフォルダ}

| paplot インストールコマンドを実行します。
| Windowsの場合、1．による python のインストール作業では環境変数 (PATH) が設定されていません。
| ここでは python をパスごと指定していますが、システム環境変数の PATH に登録することで省略することもできます。

.. caution::

  以下、python のパスは WinPython-64bit-2.7.10.3 を標準インストールしたときのものです。
  実際の環境に合わせてください。

.. code-block:: bash

  > C:\WinPython-64bit-2.7.10.3\python-2.7.10.amd64\python.exe setup.py build install

| 続けて、テストコマンドを実行します。

.. code-block:: bash

  > C:\WinPython-64bit-2.7.10.3\python-2.7.10.amd64\python.exe paplot --version
  paplot-0.5.4

| このような表示が出れば成功です。
|
| インストールが終わったら、:doc:`quick_start` をお試しください。
|

.. |new| image:: image/tab_001.gif
