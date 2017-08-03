************************
paplot コマンド
************************

------------------------
1. 基本的な使い方
------------------------

.. code-block:: bash

  paplot subcommand [--config_file CONFIG_FILE] [--title TITLE]
                    [--ellipsis ELLIPSIS] [--overview OVERVIEW]
                    [--remarks REMARKS]
                    input output_dir project_name

|

**必ず入力する項目**

:subcommand:
  paplotのサブコマンドです。いずれかを選択します。
  
  - qc
  - ca
  - mutation
  - signature
  - pmsignature

:input:
  入力ファイルです。ワイルドカード (``*``, ``?``) を使用して複数指定することができます。その場合、最初と最後に ``"`` をつけてください。

.. code-block:: bash

  # 1ファイルだけ入力する場合
  paplot qc example/qc/SAMPLE1.qc ./test multi1 --config_file example/example.cfg
  
  # 複数ファイルを入力する場合 (, で区切る)
  paplot qc "example/qc/SAMPLE1.qc.csv,example/qc/SAMPLE2.qc.csv" ./test multi1 --config_file example/example.cfg
  
  # 複数ファイルを入力する場合 (* 使用)
  paplot qc "example/qc/*.csv" ./multi multi1 --config_file example/example.cfg


:output_dir:
  出力ディレクトリを指定します。ディレクトリ構成は :ref:`2. 出力ディレクトリ <output>` を参照してください。

:project_name:
  プロジェクト名です。出力ファイルのタイトルに使用します。

.. _output:

---------------------
2. 出力ディレクトリ
---------------------

``output_dir`` オプションで指定した場所に次の構成でファイルを出力します。

.. code-block:: bash

  {output_dir}
    ├ {project_name}
    │   └ graph_*.html      <--- 各グラフ
    │
    ├ js          <--- この4つのディレクトリはHTMLファイルを表示するために必要です。消さないでください。
    ├ layout
    ├ lib
    ├ style
    │
    └ index.html             <--- このファイルをウェブブラウザで開いてください。


出力ファイルを移動する場合は ``{output_dir}`` ごと移動してください。

それぞれのグラフの使い方は `how to use graphs <./index.html#how-to-toc>`_ を参照してください。

.. _option:

------------------------
3. コマンドオプション 
------------------------

次の項目をオプションで変更することができます。

--config_file        設定ファイルです。未指定の場合、デフォルトを使用します。
--title              グラフのタイトル
--ellipsis           グラフの短縮名。グラフのファイル名になるため、同一ディレクトリに複数ファイルを出力する際に設定すると便利です。
--overview           index.htmlに表示するグラフの概要。
--remarks            index.htmlの備考欄に出力するテキストです。未指定の場合、設定ファイル [style]セクション中、remarksオプションの値を使用します。

デフォルト値は次の通りです。

=============== =================== ============ ============================================= ==============
subcommand      title               ellipsis     overview                                      remarks
=============== =================== ============ ============================================= ==============
qc              QC graphs           qc           Quality Control of bam.                       なし
ca              CA graphs           ca           Chromosomal Aberration.                       なし
mutation        Mutation Matrix     mutation     Gene-sample mutational profiles.              なし
signature       Signature           signature    Mutational Signatures.                        なし
pmsignature     PMSignature         pmsignature  Express mutational signatures in pmsignature. なし
=============== =================== ============ ============================================= ==============

.. |new| image:: image/tab_001.gif