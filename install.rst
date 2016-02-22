************************
install
************************

| paplotは次のマシンで動作します。

 * Linux系サーバ (HGCスパコン含), Linux ディストリビューション
 * MacOS X
 * Windows

| paplotを実行するにはpython 2.7が必要です。
| (python 2.6, python 3.x は未検証)
|

.. _python:

================
1. 環境の確認
================

| MacとLinuxであればデフォルトでpythonがインストールされていると思います。
| 次のコマンドでバージョンを確認してください。
|
| macの場合はターミナル画面に入力してください。
| ターミナルはアプリケーションフォルダ -> ユーティリティフォルダ-> ターミナル.appから起動できます。
|

-------------------------
1.1 pythonのバージョン
-------------------------

.. code-block:: bash

  python --version

python 2.7.x (xは"10"等の任意の数字) と表示されればOKです。

----------------------------
1.2 python packageの確認
----------------------------

pythonで使用するパッケージの確認をします。

.. code-block:: bash
  
  python
  >>> import pandas

ここで何も表示されなければOKです。

.. code-block:: bash
  
  >>> exit()

と入力してpythonから抜けてください。

.. code-block:: bash
  
  >>> import pandas
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  ImportError: No module named pandas

このようなエラーが表示される場合は :ref:`2.3. python package のインストール <package>`  を参照してインストールしてください。

====================================
2. pythonのインストール & 環境設定
====================================

--------------------
2.1 Windowsの場合
--------------------

| winPython もしくはPython(x,y)をインストールするのが手軽だと思います。
| cygwinでも動きます。

 - winPython http://winpython.github.io/
 - Python(x,y) http://python-xy.github.io/

install後、:ref:`1. 環境の確認 <python>` のコマンドを入力して、環境を確認してください。

-----------------------
2.2 Linux系サーバの場合
-----------------------

* python 2.7以外の場合は以下をExportしてください

.. code-block:: bash

  export PYTHONHOME=/usr/local/package/python/2.7.10
  export PATH=${PYTHONHOME}/bin:~/.local/bin/:$PATH
  export LD_LIBRARY_PATH=${PYTHONHOME}/lib:${LD_LIBRARY_PATH}
  export PYTHONPATH=~/.local/lib/python2.7/site-packages

* python 2.7の場合は以下をExportしてください

.. code-block:: bash

  export PATH=~/.local/bin/:$PATH


.. _package:

-------------------------------------
2.3. python package のインストール
-------------------------------------

pandas packageがない場合は次のコマンドでインストールしてください。

.. code-block:: bash
  
  >>> import pandas
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  ImportError: No module named pandas
  >>> exit()
  $ pip install pandas --user


インストール後、正しくインストールされたか確認してください。

.. code-block:: bash

  $ python
  >>> import pandas        # <--- エラーが出ないのでOK
  >>> exit()               # <--- pythonから抜ける
  $

===================================
3. paplot のインストール
===================================

.. code-block:: bash

  cd {install したいディレクトリ}
  git clone https://github.com/Genomon-Project/paplot.git
  cd paplot
  
  # 通常のパソコンの場合
  python setup.py build install
  
  # サーバの場合
  export PATH=~/.local/bin/:$PATH
  python setup.py build install --user

インストールが終わったら、:doc:`quick_start` をお試しください。


  
