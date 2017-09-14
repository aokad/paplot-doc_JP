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

**必ず入力する項目**

:subcommand:
  paplot のサブコマンドです。いずれかを選択します。
  
  - qc
  - ca
  - mutation
  - signature
  - pmsignature

:input:
  入力ファイルです。複数ファイルを使用する場合は `データファイルが分かれている場合 <./data_common.html#suffix>`_ も参照してください。

.. code-block:: bash

  # 1ファイルだけ入力する場合
  paplot mutation {unzip_path}/example/mutation_minimal/data.csv ./tmp mutation_minimal \
  --config_file {unzip_path}/example/mutation_minimal/paplot.cfg
  
  # 複数ファイル指定する場合は , で区切る
  paplot mutation \
  {unzip_path}/example/mutation_split_file/SAMPLE00.data.csv,{unzip_path}/example/mutation_split_file/SAMPLE01.data.csv \
  ./tmp mutation_split_file1 --config_file {unzip_path}/example/mutation_split_file/paplot.cfg

  # ワイルドカードを使用して、まとめて指定することも可能
  # 最初と最後に " を付けること
  paplot mutation "{unzip_path}/example/mutation_split_file/*.csv" ./tmp mutation_split_file2 \
  --config_file {unzip_path}/example/mutation_split_file/paplot.cfg

:output_dir:
  出力ディレクトリを指定します。ディレクトリ構成は :ref:`2. 出力ディレクトリ <output>` を参照してください。

:project_name:
  プロジェクト名です。出力ファイルのタイトルに使用します。

.. _output:

---------------------
2. 出力ディレクトリ
---------------------

次の構成でファイルを出力します。

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


出力ファイルを移動する際は出力ディレクトリ全体を移動してください。
それぞれのグラフの使い方は `HOW TO USE GRAPHS <./index.html#how-to-toc>`_ を参照してください。


.. _option:

------------------------
3. コマンドオプション 
------------------------

次の項目をオプションで変更することができます。

--config_file        設定ファイルです。未指定の場合、デフォルトを使用します。
--title              グラフのタイトル
--ellipsis           グラフの短縮名。グラフのファイル名になるため、同一ディレクトリに複数ファイルを出力する際に設定すると便利です。
--overview           index.html に表示するグラフの概要。
--remarks            index.html の備考欄に出力するテキストです。未指定の場合、設定ファイル ``[style]`` セクション中、 ``remarks`` オプションの値を使用します。

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
