************************
pa_plot コマンド
************************

------------------------
1. コマンドオプション 
------------------------

.. code-block:: bash

  pa_plot {qc, sv, mutation} [-h] [--version] [--config_file CONFIG_FILE] [--remarks REMARKS] input output_dir project_name

|

**必須**

:{qc, sv, mutation}:
  paplotのサブコマンドです。どれか1つを選択します。

:input:
  入力ファイルです。ワイルドカード (``*``, ``?``) を使用して複数指定することができます。その場合、最初と最後に ``"`` をつけてください。

.. code-block:: bash

  # 1ファイルだけ入力する場合
  pa_plot qc example/qc/SAMPLE1.qc ./test multi1 --config_file example/example.cfg
  
  # 複数ファイルを入力する場合 (, で区切る)
  pa_plot qc "example/qc/SAMPLE1.qc.csv,example/qc/SAMPLE2.qc.csv" ./test multi1 --config_file example/example.cfg
  
  # 複数ファイルを入力する場合 (* 使用)
  pa_plot qc "example/qc/*.csv" ./multi multi1 --config_file example/example.cfg


:output_dir:
  出力ディレクトリを指定します。ディレクトリ構成は :ref:`2. 出力ディレクトリ <output>` を参照してください。

:project_name:
  プロジェクト名です。出力ファイルのタイトルに使用します。

**任意**

--config_file        設定ファイルです。未指定の場合、デフォルトを使用します。
--remarks            index.htmlの備考欄に出力するテキストです。未指定の場合、設定ファイルの値を使用します。
-h                   ヘルプを表示します。
--version            バージョンを表示します。

.. _output:

---------------------
2. 出力ディレクトリ
---------------------

``output_dir`` オプションで指定した場所に次の構成でファイルを出力します。

.. code-block:: bash

  {output_dir}
    ├ {project_name}
    │   ├ graph_mut.html    <--- mutation-matrix グラフ
    │   ├ graph_qc.html     <--- qc グラフ
    │   └ graph_sv.html     <--- sv グラフ
    │
    ├ js          <--- この4つのディレクトリはHTMLファイルを表示するために必要です。消さないでください。
    ├ layout
    ├ lib
    ├ style
    |
    └ index.html             <--- このファイルを web ブラウザで開いてください。


出力ファイルを移動する場合は ``{output_dir}`` ごと移動してください。

出力ファイルの操作方法は :doc:`how to use graphs<use_graph>` を参照してください。

