*******************************
Config 記述方法 (CA)
*******************************

全設定項目
---------------------------------

.. code-block:: cfg
  :linenos:
  :emphasize-lines: 10,46,48,49,50,56,57,58,59,71
  
  ###################### sv
  [genome]
  # ゲノムサイズのファイル（CSV形式）（デフォルトはhg19, installディレクトリ配下のgenomeディレクトリにあります）
  #
  # for example.
  # (linux)
  # path = ~/tmp/genome/hg19.csv
  # (windows)
  # path = C:\genome\hg19_part.csv
  path = 
  
  [ca]
  # 使用するchromosomes (,で区切る)
  use_chrs = 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,X,Y
  
  # if setting label-text & color
  # use_chrs = 1:Chr1:crimson, 2:Chr2:lightpink, 3:Chr3:mediumvioletred, 4:Chr4:violet, 5:Chr5:darkmagenta, 6:Chr6:mediumpurple
  
  # 積み上げグラフのchromosome分割サイズ (bps)
  selector_split_size = 5000000
  
  ##################
  # group setting
  # [result_format_ca] col_opt_group が設定されている場合のみ有効
  ##################
  
  # 入力されていた場合、そのgroupのみ出力する
  # 未入力の場合、検出されたgroupすべて出力する
  # , 区切りで複数指定可能
  #
  limited_group = stopgain,frameshift_deletion,frameshift_insertion
  
  # 入力されていた場合、そのgroupはplot対象から除外する
  # , 区切りで複数指定可能
  # 空白行を除去する場合、_blank_ と記入する
  nouse_group = _blank_,unknown,synonymous_SNV
  
  # groupのplot色を指定する。group名:(RGBもしくはカラー名)
  # , 区切りで複数指定可能
  # 未入力のgroupはデフォルト色を使用する
  group_colors = stopgain:#E85299,frameshift_deletion:#F39600,frameshift_insertion:#E60011
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  # 項目は欄外「入力ファイルフォーマット」参照
  [result_format_ca]
  suffix = .result.txt
  
  sept = \t
  header = False
  comment = #
  
  ##################
  # Column index (required)
  ##################
  
  col_chr1 = Chr_1
  col_break1 = Pos_1
  col_chr2 = Chr_2
  col_break2 = Pos_2
  
  ##################
  # Column index (option)
  ##################
  
  col_opt_dir1 = Dir_1
  col_opt_dir2 = Dir_2
  col_opt_type = Variant_Type
  col_opt_gene_name1 = Gene_1
  col_opt_gene_name2 = Gene_2
  col_opt_group = 
  col_opt_id =
  
  # 出力フォーマット
  # 項目は欄外「出力ファイルフォーマット」参照
  [merge_format_ca]
  lack_column_complement = NA
  sept = ,


表示するchromosomeを限定する
---------------------------------

configファイルで次の項目を編集してください。

.. code-block:: cfg

  [ca]
  # 使用するchromosomes (,で区切る)
  # default
  # use_chrs = 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,X,Y
  
  # chromosome 1,5,7を使用する場合
  use_chrs = 1,5,7

編集したconfigファイルは次のようにしてコマンドから指定します。

``paplot {input files} {output directory} {title} --config_file {config file}``


ヒト以外のゲノムを使用する
-------------------------------

genomeサイズが入力されたファイルが必要です。

先頭列にchromosome名、2列目にサイズをカンマ ``,`` もしくはタブ区切りで入力してください。

.. code-block:: cfg
  
  1,249250621
  2,243199373
  3,198022430
  7,159138663
  8,146364022
  X,141213431
  Y,135534747
  9_gl000201_random,36148
  11_gl000202_random,40103
  17_gl000204_random,81310
  17_gl000205_random,174588
  Un_gl000214,137718

chromosome名は分析したいファイルのChr1, Chr2で使用されている名称と同じでなければなりません。

.. image:: image/qa_genome_size.PNG

用意したゲノムサイズのファイルをconfig fileに指定してください。

.. code-block:: cfg

  [genome]
  # ゲノムサイズのファイル（CSV形式）（デフォルトはhg19, installディレクトリ配下のgenomeディレクトリにあります）
  #
  # for example.
  # (linux)
  # path = ~/tmp/genome/hg19.csv
  # (windows)
  # path = C:\genome\hg19_part.csv
  path = {ここにゲノムサイズのファイルのパスを指定する}


ポップアップウィンドウの表示内容
----------------------------------------

| 記載方法は :ref:`ユーザ定義フォーマット<user_format>` を参照してください。
| SVにはmutation-matrixのような特殊キーワードはありません。
|


.. |new| image:: image/tab_001.gif
