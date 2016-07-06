************************
install
************************

| paplotは次のマシンで動作します。
|

 * Linux系サーバ (HGCスパコン含), Linux ディストリビューション
 * MacOS X
 * Windows

| paplotを実行するにはpython 2.7が必要です。
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
  git clone -b master https://github.com/Genomon-Project/paplot.git
  cd paplot

  python setup.py build install
  
  # 上のコマンドでエラーが出る場合
  export PATH=~/.local/bin/:$PATH
  export LD_LIBRARY_PATH=~/.local/lib/:$LD_LIBRARY_PATH
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

.. note::
  
  PATH設定を忘れないようにする
  
  | ↑でexport設定したPATHとLD_LIBRARY_PATHはログアウトすると忘れてしまいます。
  | 再ログイン時に再設定されるよう設定ファイルに記入しておくことをお勧めします。
  | ``~/.bashrc`` もしくは ``~/.bash_profile`` ファイルに次の2行を記入してください。
  |

  .. code-block:: bash
  
    export PATH=~/.local/bin/:$PATH
    export LD_LIBRARY_PATH=~/.local/lib/:$LD_LIBRARY_PATH
  


================================================
MacOS Xの場合
================================================

1. ソースファイルのダウンロード
------------------------------------

| paplotのサイトから最新版の ``Source code (zip)`` をダウンロードします。
|

https://github.com/Genomon-Project/paplot/releases/

| ``git`` コマンドが使える方は ``git clone -b master https://github.com/Genomon-Project/paplot.git`` でもよいです。
|

2. paplot のインストール
--------------------------

| ターミナルを起動してダウンロードしたディレクトリに移動します。
| 
| 「ターミナル.app」がDockの中にない場合、次からたどることができます。
| Finder → 「移動」メニュー → 「アプリケーション」を選択 → 「ユーティリティ」ディレクトリを開く → 「ターミナル」を起動
| 
| <user name>は自分のユーザ名です。
| ``whoami`` コマンドで確認できます。
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

| このままではターミナルは ``pa_plot`` がどこにあるかわからないので、インストールされているところにPATHを通します。
| 大抵、ここにあります。
|

``/Users/<user name>/Library/Python/2.7/bin``

.. note::

  | ここにない場合は ``find / -name pa_plot`` とコマンドを入力してインストールされているところを探します。
  |
  | 4つ見つかるはずです。
  | このうち、downloadしたディレクトリは使用しません。
  | 

  .. code-block:: bash
    
    {installしたディレクトリ}/bin/pa_plot               <--- ココです
    {installしたディレクトリ}/lib/python2.7/site-packages/paplot-0.2.6devel-py2.7.egg/EGG-INFO/scripts/pa_plot
    {downloadディレクトリ}/paplot-devel/pa_plot
    {downloadディレクトリ}/paplot-devel/build/scripts-2.7/pa_plot
  

.. code-block:: bash

  export PATH={installしたディレクトリ}/bin:$PATH
  export LD_LIBRARY_PATH={installしたディレクトリ}/lib:$LD_LIBRARY_PATH
  
  # 大抵は以下でOKです。
  # <user name>は自分のユーザ名に置き換えてください。
  # export PATH=/Users/<user name>/Library/Python/2.7/bin:$PATH
  # export LD_LIBRARY_PATH=/Users/<user name>/Library/Python/2.7/lib:$LD_LIBRARY_PATH


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

.. note::
  
  PATH設定を忘れないようにする
  
  | ↑で設定したPATHは再起動すると忘れてしまうので、
  | 起動するたびに ``export PATH=...`` コマンドを入力する必要があります。
  | ここでは、起動しても自動的に再設定されるようにします。
  |
  | 設定ファイルを作成します。
  |
  
  .. code-block:: bash
  
    vi ~/.bash_profile
  
  | ファイルが開いたら ``i`` と入力して編集モードにします。
  | ファイルにすでに何か記入されていたら ``↓`` キーで最後の行に移動します。
  | 
  | <user name>は自分のユーザ名です。
  |
  
  .. code-block:: bash
  
    export PATH=/Users/<user name>/Library/Python/2.7/bin:$PATH
    export LD_LIBRARY_PATH=/Users/<user name>/Library/Python/2.7/lib:$LD_LIBRARY_PATH
  
  | PATHの設定で入力したものと同じパスを入力してください。
  | 入力したら ``ESC`` キーを押して、編集モードから抜けます。その後、``:wq`` と入力して保存して終了します。
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

| python 2.7.10 で動作確認済みです。
| 

2. paplot のインストール
-----------------------------

| paplotのサイトから最新版の ``Source code (zip)`` をダウンロードします。
| ダウンロードしたファイルは適当なフォルダに解凍します。
|

https://github.com/Genomon-Project/paplot/releases/

| インストールしたフォルダにコマンドプロンプトがありますので、起動します。
| WinPython-64bit-3.5.1.2 を標準でインストールした場合、ここにあります。
| 

``C:\\Program Files\\\WinPython-64bit-2.7.10.2\\WinPython Command Prompt.exe``

| 起動した画面に以下を入力します。
| 

.. code-block:: bash

  cd {zipを解凍したフォルダ}
  python setup.py build install


| Windowsの場合、 ``pa_plot`` コマンドにパスが通っていないのでバッチファイルを使用します。
| zipを解凍したフォルダに ``pa_plot.cmd`` がありますので、ノートパッド等テキストエディタで開いて編集します。
| 

.. code-block:: bash

  set pa_plot="C:\Program Files\WinPython-64bit-2.7.10.2\python-2.7.10.amd64\Scripts\pa_plot"

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
| 以降、``pa_plot`` コマンドは ``pa_plot.cmd`` と読み替えてください。
| 
| インストールが終わったら、:doc:`quick_start` をお試しください。
| 

