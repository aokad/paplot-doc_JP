************************
install
************************

| paplotを実行するにはpython 2.7が必要です。
| (python 2.6, python 3.x は未検証)
|
|
| paplotは次のマシンで動作します。

 * Linux系サーバ (HGCスパコン含), Linux ディストリビューション
 * MacOS X
 * Windows

1. 環境の確認
================

| MacとLinuxであればデフォルトでpythonがインストールされていると思います。
| 次のコマンドでバージョンを確認してください。
|
| macの場合はターミナル画面に入力してください。
| ターミナルはアプリケーションフォルダ -> ユーティリティフォルダ-> ターミナル.appから起動できます。


1.1 pythonのバージョン
-------------------------

.. code-block:: bash

  python --version

python 2.7.xと表示されればOKです。

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

2. pythonのインストール & 環境設定
====================================

2.1 Windowsの場合
--------------------

| winPython もしくはPython(x,y)をインストールするのが手軽だと思います。
| cygwinでも動きます。

 - winPython http://winpython.github.io/
 - Python(x,y) http://python-xy.github.io/

install後、1.のコマンドを入力して、環境を確認してください。

2.2 HGCスパコンの場合
-----------------------

# python 2.7以外の場合は以下をExportしてください

.. code-block:: bash

  export PYTHONHOME=/usr/local/package/python/2.7.10
  export PATH=${PYTHONHOME}/bin:$PATH
  export LD_LIBRARY_PATH=${PYTHONHOME}/lib:${LD_LIBRARY_PATH}
  export PYTHONPATH=~/.local/lib/python2.7/site-packages
 
3. python package のインストール
===================================

pandas packageがない場合は次のコマンドでインストールしてください。

.. code-block:: bash

  pip install pandas

4. paplot のインストール
===================================

.. code-block:: bash

  cd {install したいディレクトリ}
  git clone https://github.com/Genomon-Project/paplot.git
  cd paplot
  
  # 通常のパソコンの場合
  python setup.py build install
  
  # サーバの場合
  python setup.py build install --user

インストールが終わったら、:ref:`quick_start` をお試しください。


  
