************************
pa_plot コマンド
************************

------------------------
1. コマンドオプション 
------------------------

.. code-block:: bash

  pa_plot {qc, sv} [-h] [--version] [--config_file CONFIG_FILE] input output_dir project_name

|

必須

* :command:`{qc, sv}`

  paplotのサブコマンドです。どちらかを選択します。

* :command:`input`

  入力ファイルです。ワイルドカード (:command:`*`) を使用して複数指定することができます。最初と最後に :command:`"` をつけてください。

* :command:`output_dir`

  出力ディレクトリを指定します。ディレクトリ構成は :ref:`2. 出力ディレクトリ <output>` 参照してください。

* :command:`project_name`

  プロジェクト名です。出力ファイルのタイトルに使用します。

任意

* :command:`--config_file`

  設定ファイルです。未指定の場合、デフォルトを使用します。

その他

* :command:`-h`

  ヘルプを表示します。

* :command:`--version`

  バージョンを表示します。


.. _output:

---------------------
2. 出力ディレクトリ
---------------------

:command:`output_dir` オプションで指定した場所に次の構成でファイルを出力します。

.. code-block:: bash

{output_dir}
  ├ {project_name}
  │   ├ graph_qc.html     <--- qc グラフ 
  │   └ graph_sv.html     <--- sv グラフ
  │
  ├ js          <--- この3つのディレクトリはHTMLファイルを表示するために必要です。消さないでください。
  ├ lib
  └ style


出力ファイルを移動する場合は{output_dir}ごと移動してください。

--------------------
3. 出力ファイル
--------------------

3-1. graph_qc.html
-----------------------

qcグラフは次のようにしてデータのソートや拡大ができます。

.. image:: image/qc_operation.PNG
  :scale: 100%

3-2. graph_sv.html
-----------------------

svグラフは次のようにしてデータの詳細表示ができます。

.. image:: image/sv_operation.PNG
  :scale: 100%

