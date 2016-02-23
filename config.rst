**************************
自分のデータを使用する
**************************

configファイルを編集することで自分のデータを使用できます。

configファイルのサンプルは以下にあります。

:doc:`{paplotをインストールしたディレクトリ}/example/example.cfg`

.. code-block:: cfg

  [genome]
  # ゲノムサイズのファイル（CSV形式）（デフォルトはhg19, installディレクトリ配下のgenomeディレクトリにあります）
  #
  # for example.
  # (linux)
  # path = ~/tmp/genome/hg19.csv
  # (windows)
  # path = C:\genome\hg19_part.csv
  path = 
  
  [style]
  # グラフのレイアウトファイル
  # ~/tmp/paplot/style/rainbow.js
  path = 
  
  [sv]
  # 使用するchromosomes (,で区切る)
  use_chrs = 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,X,Y
  
  [qc]
  # qcでどのグラフを表示するか (表示しない場合Falseにする)
  chart_coverage=True
  chart_average=True
  chart_mapped=True
  chart_insert=True
  chart_duplicate=True
  chart_length=True
  
  [result_format_sv]
  # sv の入力ファイルフォーマット
  
  # suffix (col_pos_IDが指定されていない場合、suffix以前をIDとする)
  suffix = .result.txt

  # データ区切り(タブ区切りの場合)
  sept = \t
  # ,区切りの場合
  sept = ,
  # スペース区切りの場合
  sept = " "
  
  # 先頭1行がヘッダかどうか (先頭行がヘッダの場合はTrue)
  header = False
  
  # データ列の位置
  #col_pos_ID =
  col_pos_chr1 = 0
  col_pos_start = 1
  col_pos_dir1 = 2
  col_pos_chr2 = 3
  col_pos_end = 4
  col_pos_dir2 = 5
  col_pos_type = 8
  col_pos_gene_name1 = 9
  col_pos_gene_name2 = 10
  
  [result_format_qc]
  # qc の入力ファイルフォーマット
  # (svとほぼ同)

suffixとID

.. image:: image/id_suffix.PNG
  :scale: 100%

列と設定の対応
=========================

.. image:: image/col_pos.PNG
  :scale: 100%
  

** SVの場合 **

====================  ===============  =============================
name                  input type       description
====================  ===============  =============================
col_pos_ID            text             サンプルを識別できる名称
col_pos_chr1          text             chromosome of break point 1
col_pos_start         numeric          position of break point 1
col_pos_dir1          text             direction of break point 1
col_pos_chr2          text             chromosome of break point 2
col_pos_end           numeric          position of break point 2
col_pos_dir2          text             direction of break point 2
col_pos_type          text             type of variation
col_pos_gene_name1    text             gene name of break point 1
col_pos_gene_name2    text             gene name of break point 2
====================  ===============  =============================

** QCの場合 **

========================  =============  =============================
name                      input type     description
========================  =============  =============================
col_pos_ID                text           サンプルを識別できる名称
col_pos_total_reads       numeric        number of total reads
col_pos_mapped_reads      numeric        number of mapped reads
col_pos_duplicate_reads   numeric        number of duplicate reads
col_pos_mean_insert_size  numeric        mean of insert size
col_pos_average_depth     numeric        average of depth
col_pos_read_length_r1    numeric        number of read_length_r1
col_pos_read_length_r2    numeric        number of read_length_r2
col_pos_ratio_2x          0.0～1.0       coverage (depth=2)
col_pos_ratio_10x         0.0～1.0       coverage (depth=10)
col_pos_ratio_20x         0.0～1.0       coverage (depth=20)
col_pos_ratio_30x         0.0～1.0       coverage (depth=30)
========================  =============  =============================


作成したconfigファイルはpa_plot コマンドの--config_file オプションで指定します。

実行例

.. code-block:: bash

  pa_plot qc "example/qc/*.csv" ./tmp DUMMY --config_file example/example.cfg

