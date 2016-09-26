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
  paplotのサブコマンドです。いづれかを選択します。(svはCAグラフを出力します)

:input:
  入力ファイルです。ワイルドカード (``*``) を使用して複数指定することができます。最初と最後に ``"`` をつけてください。

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
    │   └ graph_ca.html     <--- ca グラフ
    │
    ├ js          <--- この3つのディレクトリはHTMLファイルを表示するために必要です。消さないでください。
    ├ lib
    ├ style
    └ index.html             <--- このファイルを web ブラウザで開いてください。


出力ファイルを移動する場合は ``{output_dir}`` ごと移動してください。

出力ファイルの操作方法は :doc:`how to use graphs<use_graph>` を参照してください。

