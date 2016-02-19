========================================
paplotによるグラフ作成
========================================

#. paplotをインストール
#. testサンプルでコマンドを実行
#. 結果ファイルを表示

1. paplotをインストール
^^^^^^^^
| HGCスパコンで使用される場合、事前に`qlogin`してください。
|

.. code-block:: bash

  git clone https://github.com/Genomon-Project/paplot.git
  cd paplot

  python setup.py build install --user

| installの確認
| 以下を入力してください。
| 

.. code-block:: bash

  pa_plot conf

| 以下が表示されればインストール成功です。
| 

.. code-block:: bash

  **********************
     hello paplot !!!
  **********************
  (このあとにデフォルト設定の内容が表示されます)


2. testサンプルでコマンドを実行
^^^^^^^^

テストサンプルを用意していますので実行します。

.. code-block:: bash

  cd {paplotをインストールしたディレクトリ}

  # create bar graphs of qc
  pa_plot qc "example/qc/*.csv" ./tmp DUMMY --config_file example/example.cfg

  # create bundle graphs of Structural Variation (SV)
  pa_plot sv "example/sv/*.txt" ./tmp DUMMY --config_file example/example.cfg


3. 結果ファイルを表示
^^^^^^^^

次の場所にHTMLファイルが2つできていますか？

.. code-block:: bash
  {paplot をインストールしたディレクトリ}
    └ tmp
        ├ DUMMY
        │   ├ <font color=red>graph_qc.html</font>
        │   └ <font color=red>graph_sv.html</font>
        │
        ├ js
        ├ lib
        └ style


| web ブラウザで開いてください。
| ※HGCスパコン等、サーバ上で実行した場合はファイルをローカルに転送するか、サーバ上の仮想ウィンドウ(NoMachime等)で表示してください。
| 
| 次のように見えていますか?

.. image:: image/genomon_kun.png
.. image:: image/logo.png








