--------------------------------
install
--------------------------------

| paplotの実python 2.7が必要です。
| (python 2.6, python 3.x は未検証)
|

 * Linux系サーバ (HGCスパコン含), Linux ディストリビューション
 * MacOS X
 * Windows

1. 環境の確認

| MacとLinuxであればデフォルトでpythonがインストールされていると思います。
| 次のコマンドでバージョンを確認してください。
|
| macの場合はターミナルを起入力してください。
| アプリケーションフォルダ -> ユーティリティフォルダ-> ターミナル.appから起動できます。

1.1 pythonのバージョン

.. code-block:: bash

  $ python --version
  python 2.7.10

python 2.7.xと表示されればOKです。

1.2 python packageの確認

pythonで使用するパッケージの確認をします。

.. code-block:: bash

  $ python
  >>> import pandas

ここで何も表示されなければOKです。

2. pythonのインストール

1.1でNだった
  

1. Python install



1. 環境設定
^^^^^^^^^^^^^^^^
1-1. pythonの環境設定
Genomonではpythonバージョン2.7を使用します.

.. code-block:: bash


  # python 2.7以外の場合は以下をExportしてください
  export PYTHONHOME=/usr/local/package/python/2.7.10
  export PATH=${PYTHONHOME}/bin:$PATH
  export LD_LIBRARY_PATH=${PYTHONHOME}/lib:${LD_LIBRARY_PATH}
  export PYTHONPATH=~/.local/lib/python2.7/site-packages
 
