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

 * :ref:`Linux系の場合 (MacOS X, HGCスパコン, cygwin含) <linux>`
 * :ref:`Windowsの場合 <windows>`

.. _linux:

================================================
Linux系の場合 (MacOS X, HGCスパコン, cygwin含)
================================================

1. PATHの設定 (サーバのみ)
-----------------------------

* 以下をExportしてください

.. code-block:: bash

  export PATH=~/.local/bin/:$PATH


2. python packageの確認, install
-----------------------------------

| MacとLinuxであればデフォルトでpythonがインストールされていると思います。
| 次のコマンドで使用するパッケージがインストールされているか確認してください。
|
| macの場合はターミナル画面に入力してください。
| ターミナルはアプリケーションフォルダ -> ユーティリティフォルダ-> ターミナル.appから起動できます。
|
| pythonで使用するパッケージの確認をします。

.. code-block:: bash
  
  python
  >>> import pandas

| ここで何も表示されなければOKです。

.. code-block:: bash
  
  >>> exit()

| と入力してpythonから抜けてください。

.. code-block:: bash
  
  >>> import pandas
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  ImportError: No module named pandas

| このようなエラーが表示される場合は次のコマンドでインストールしてください。

.. code-block:: bash
  
  >>> exit()
  
  # パソコンの場合
  $ pip install pandas
  # サーバの場合
  $ pip install pandas --user


| インストール後、正しくインストールされたか確認してください。

.. code-block:: bash

  $ python
  >>> import pandas        # <--- エラーが出ないのでOK
  >>> exit()               # <--- pythonから抜ける
  $


3. paplot のインストール
--------------------------

.. code-block:: bash

  cd {install したいディレクトリ}
  git clone https://github.com/Genomon-Project/paplot.git
  cd paplot
  
  # パソコンの場合
  python setup.py build install
  
  # サーバの場合
  export PATH=~/.local/bin/:$PATH
  python setup.py build install --user
  
  pa_plot conf
  **********************
     hello paplot !!!
  **********************

  (デフォルト設定値が表示される)

| このような表示が出れば成功です。

| インストールが終わったら、:doc:`quick_start` をお試しください。
| 

.. _windows:

====================================
Windows系の場合
====================================

1. Pythonのインストール
---------------------------

| winPython もしくはPython(x,y)をインストールするのが手軽だと思います。
| cygwinでも動きます。
| cygwinの場合は :ref:`Linux系の場合 (MacOS X, HGCスパコン, cygwin含) <linux>` を参照してください。
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

