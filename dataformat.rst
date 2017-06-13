**************************
データフォーマット
**************************

ここでは、exampleデータ (※) を基にして、それぞれのレポートを出力するために必要な入力データを解説します。

※ exampleデータはpaplotをダウンロードして解凍したディレクトリ中、exampleディレクトリにあります。

.. _conf_mm:

1. mutation-matrix
----------------------

======================
exampleデータ
======================

`example/mutation/sample_merge.csv` 

.. raw:: html

  <div style="margin-top: 10px; margin-bottom: 10px; padding: 8px; border: 1px solid #AAA; background-color:#FFF; ">
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><b><font color="red">ID</font>,Chr,Start,End,Ref,Alt,<font color="red">func,gene</font></b></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE00</font>,chr10,8114472,8114474,A,C,<font color="red">intronic,GATA3</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE00</font>,chr13,28644892,28644901,G,-,<font color="red">intronic,FLT3</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE00</font>,chr13,28664636,28664638,-,G,<font color="red">intronic,FLT3</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE01</font>,chr16,68795521,68795530,-,T,<font color="red">UTR3,CDH1</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE01</font>,chr10,8117068,8117069,G,T,<font color="red">exonic,GATA3</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE02</font>,chr3,178906688,178906688,G,A,<font color="red">intronic,PIK3CA</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE02</font>,chr13,28603715,28603715,G,-,<font color="red">intergenic,FLT3</font></p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'><font color="red">SAMPLE03</font>,chr14,103368263,103368270,G,C,<font color="red">intronic,TRAF3</font></p>
  </div>

exampleデータでは変異ファイルの例として、上記のデータを用意しています。

 - 赤字で記載したサンプルid(ID), func(変異タイプ), gene(遺伝子名）の3つが必須項目です。
 - 太字がヘッダ名です。configファイルの [result_format_mutation] セクションでヘッダ名を指定します。

`example/paplot.cfg` 

.. code-block:: cfg

  ###################### mutation
  # 入力フォーマット (自分のデータに合わせて変更する)
  [result_format_mutation]
  sept = ,
  header = True
  
  ##################
  # Column index (required)
  ##################

  # 変異タイプ
  col_func = func
  # 遺伝子名
  col_gene = gene
  
  ##################
  # column index (option)
  ##################
  
  # chromosome
  col_opt_chr = Chr
  # 開始位置
  col_opt_start = Start
  # 終了位置
  col_opt_end = End
  # リファレンスの塩基配列
  col_opt_ref = Ref
  # 対象の塩基配列
  col_opt_alt = Alt
  # id (sample) 列
  col_opt_ID = id

==========================
最小データセット
==========================

paplotに最低限必要な項目のみで構成した、以下のようなデータがあるとします。

.. raw:: html

  <div style="margin-top: 10px; margin-bottom: 10px; padding: 8px; border: 1px solid #AAA; background-color:#FFF;">
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>ID,func,gene</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,intronic,GATA3</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,intronic,FLT3</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,intronic,FLT3</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,UTR3,CDH1</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,exonic,GATA3</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,intronic,PIK3CA</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,intergenic,FLT3</p>
  <p style='margin-top: 1px; margin-bottom: 1px; font-size: 12px; font-family: Consolas,"Andale Mono WT","Andale Mono","Lucida Console","Lucida Sans Typewriter","DejaVu Sans Mono","Bitstream Vera Sans Mono","Liberation Mono","Nimbus Mono L",Monaco,"Courier New",Courier,monospace;'>SAMPLE00,intronic,TRAF3</p>
  </div>

configファイルは以下のようになります。

ハイライト表示が変更箇所です。

.. code-block:: cfg
  :emphasize-lines: 25,45,46,47,48,49
  
  ###################### general
  [style]
  path = 
  remarks = 
  
  ###################### mutation
  [mutation]
  use_gene_rate = 0
  
  limited_genes = 
  nouse_genes = 
  limited_funcs = 
  nouse_funcs = 
  func_colors = 
  
  ### special item
  # {#number_id}
  # {#number_gene}
  # {#number_mutaion}
  # {#sum_mutaion}
  # {#item_value}
  # {#sum_item_value}
  
  tooltip_format_checker_title1 = ID:{id}, gene:{gene}, {#sum_item_value}
  tooltip_format_checker_partial = type[{func}]
  tooltip_format_gene_title = gene:{gene}, {#sum_item_value}
  tooltip_format_gene_partial = func:{func}, {#item_value}
  tooltip_format_id_title = ID:{id}, {#sum_item_value}
  tooltip_format_id_partial = func:{func}, {#item_value}
  
  [result_format_mutation]
  suffix = 
  
  sept = ,
  header = True
  comment = #
  sept_func = ;
  sept_gene = ;
  
  # column index (required)
  col_func = func
  col_gene = gene
  
  # column index (option)
  col_opt_chr = 
  col_opt_start = 
  col_opt_end = 
  col_opt_ref = 
  col_opt_alt = 
  col_opt_id = ID
  
  [merge_format_mutation]
  lack_column_complement = NA
  sept = ,


作成したconfigファイルは ``paplot`` コマンドの ``--config_file`` オプションで指定します。

実行例

.. code-block:: bash

  paplot mutation {/path/to/data.csv} ./tmp MINIMAL --config_file example/paplot.cfg


1. 全般
------------

.. code-block:: cfg
  :linenos:

  ###################### general
  [style]
  # グラフのレイアウトファイル
  # ~/tmp/paplot/style/rainbow.js
  path = 
  
  # index.html の備考欄に出力するテキスト(HTMLタグ使用可, 半角英数字のみ)
  remarks = 

.. _conf_qc:

2. QC
------------

出力するグラフを変更しない場合は、[result_format_qc] のみ自分のデータに合わせて設定してください。

:ref:`入力ファイルフォーマット<data_format>` に各項目の解説を記載しています。

QCグラフ固有の設定記載方法について、詳細は :doc:`config_qc` に記載しています。

.. code-block:: cfg
  :linenos:
  :emphasize-lines: 8,10,11,12,24,25,26,27,28,29,30,31,32,33,34,35
  
  ###################### qc
  [qc]
  # (none)
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  # 各項目の解説はページ下段の「入力ファイルフォーマット」に記載
  [result_format_qc]
  suffix = .qc.csv
  
  sept = ,
  header = True
  comment = #
  
  ##################
  # Column index (required)
  ##################
  
  # (none)
  
  ##################
  # Column index (option)
  ##################
  
  col_opt_duplicate_reads = duplicate_reads
  col_opt_mapped_reads = mapped_reads
  col_opt_total_reads = total_reads
  col_opt_average_depth = average_depth
  col_opt_mean_insert_size = mean_insert_size
  col_opt_ratio_2x = 2x_rt
  col_opt_ratio_10x = 10x_rt
  col_opt_ratio_20x = 20x_rt
  col_opt_ratio_30x = 30x_rt
  col_opt_read_length_r1 = read_length_r1
  col_opt_read_length_r2 = read_length_r2
  col_opt_id = file_name
  
  # 出力フォーマット
  # 各項目の解説はページ下段の「出力ファイルフォーマット」に記載
  [merge_format_qc]
  lack_column_complement = NA
  sept = ,
  
  # 領域選択用のグラフ設定
  [qc_chart_brush]
  title = 
  title_y = 
  stack = {average_depth}
  name_set = average:#E3E5E9
  tooltip_format = 
  
  # グラフ設定(グラフごとに用意する)
  [qc_chart_1]
  title = depth coverage
  title_y = coverage
  stack1 = {ratio_30x}
  stack2 = {ratio_20x-ratio_30x}
  stack3 = {ratio_10x-ratio_20x}
  stack4 = {ratio_2x-ratio_10x}
  name_set = ratio_30x:#2478B4, ratio_20x:#FF7F0E, ratio_10x:#2CA02C, ratio_2x:#D62728
  tooltip_format1 = ID:{id}
  tooltip_format2 = ratio_2x: {ratio_2x:.2}
  tooltip_format3 = ratio_10x: {ratio_10x:.2}
  tooltip_format4 = ratio_20x: {ratio_20x:.2}
  tooltip_format5 = ratio_30x: {ratio_30x:.2}

.. _conf_ca:

3. CA
--------------

出力するグラフを変更しない場合は、[result_format_ca] のみ自分のデータに合わせて設定してください。

:ref:`入力ファイルフォーマット<data_format>` に各項目の解説を記載しています。

CAグラフ固有の設定記載方法について、詳細は :doc:`config_ca` に記載しています。

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

.. _conf_mm:

4. mutation-matrix
----------------------

出力するグラフを変更しない場合は、[result_format_mutation] のみ自分のデータに合わせて設定してください。

:ref:`入力ファイルフォーマット<data_format>` に各項目の解説を記載しています。

mutation-matrixグラフ固有の設定記載方法について、詳細は :doc:`config_mat` に記載しています。

.. code-block:: cfg
  :linenos:
  :emphasize-lines: 50,51,52,53,56,58,65,68,75,77,79,81,83,85

  ###################### mutation
  [mut]
  # geneのサンプルに対する検出比(%) 
  # 値より小さいgeneはplot対象から除外する
  # 0の場合はすべて出力する
  use_gene_rate = 0

  # 入力されていた場合、そのgeneのみ出力する
  # 未入力の場合、検出されたgeneすべて出力する
  # , 区切りで複数指定可能
  #
  # limited_genes = TP,TTN,APC,BRAF,CDH1,FLT3
  limited_genes = 
  
  # 入力されていた場合、そのgeneはplot対象から除外する
  # , 区切りで複数指定可能
  #
  # nouse_genes = NONE,MUC4
  nouse_genes =

  # 入力されていた場合、その変異タイプ(func)のみ出力する
  # 未入力の場合、検出されたfuncすべて出力する
  # , 区切りで複数指定可能
  #
  # limited_funcs = exome,splicing
  limited_funcs = 
  
  # 入力されていた場合、そのfuncはplot対象から除外する
  # , 区切りで複数指定可能
  # 空白行を除去する場合、_blank_ と記入する
  nouse_funcs = _blank_,unknown,synonymous_SNV
  
  # funcのplot色を指定する。func名:(RGBもしくはカラー名)
  # , 区切りで複数指定可能
  # 未入力のfuncはデフォルト色を使用する
  func_colors = stopgain:#E85299,frameshift_deletion:#F39600,frameshift_insertion:#E60011,nonframeshift_deletion:#9CAEB7
  
  # ポップアップウィンドウの表示内容
  # 詳細はページ下段の「ユーザ定義フォーマット」に記載
  tooltip_format_checker_title1 = ID:{id}, gene:{gene}, {#sum_item_value}
  tooltip_format_checker_partial = type[{func}], {chr}:{start}:{end}, [{ref} -----> {alt}]
  tooltip_format_gene_title = gene:{gene}, {#sum_item_value}
  tooltip_format_gene_partial = func:{func}, {#item_value}
  tooltip_format_id_title = ID:{id}, {#sum_item_value}
  tooltip_format_id_partial = func:{func}, {#item_value}
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  # 項目は欄外「入力ファイルフォーマット」参照
  [result_format_mutation]
  suffix = 
  sept = \t
  header = True
  comment = #
  
  # funcが1セルに複数入力されている場合の区切り文字
  sept_func = ";"
  # geneが1セルに複数入力されている場合の区切り文字
  sept_gene = ";"
  
  ##################
  # Column index (required)
  ##################

  # func列
  col_func = Merge_Func
  
  # gene列
  col_gene = Gene.refGene
  
  ##################
  # column index (option)
  ##################
  
  # chromosome
  col_opt_chr = Chr
  # 開始位置
  col_opt_start = Start
  # 終了位置
  col_opt_end = End
  # リファレンスの塩基配列
  col_opt_ref = Ref
  # 対象の塩基配列
  col_opt_alt = Alt
  # id (sample) 列
  col_opt_ID = id
  
  # 出力フォーマット
  # 項目は欄外「出力ファイルフォーマット」参照
  [merge_format_mutation]
  lack_column_complement = NA
  sept = ,

.. _conf_signature:

5. signature
---------------------------

:doc:`exec_signature` の手順で実行する場合、configファイルの変更は必要ありません。

signatureデータ準備方法およびjsonファイルフォーマットについては :doc:`exec_signature` に記載しています。

.. code-block:: cfg
  :linenos:
  
  ###################### signature
  [signature]

  # ポップアップウィンドウの表示内容
  # 詳細はページ下段の「ユーザ定義フォーマット」に記載
  tooltip_format_signature_title = {sig}
  tooltip_format_signature_partial = {route}: {#sum_item_value:6.2}
  tooltip_format_mutation_title = {id}
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
  # signatureのY軸最大値 (-1の場合、それぞれのデータの最大値を使用する)
  signature_y_max = -1
  
  # signatureのbarの色
  alt_color_CtoA = #1BBDEB
  alt_color_CtoG = #211D1E
  alt_color_CtoT = #E62623
  alt_color_TtoA = #CFCFCF
  alt_color_TtoC = #ACD577
  alt_color_TtoG = #EDC7C4
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  [result_format_signature]

  # 入力形式 (現在はjsonのみ)
  format = json

  # background を使用しているかどうか
  background = True
  
  # jsonファイルのkey名
  key_id = id
  key_mutation = mutation
  key_signature = signature
  key_mutation_count = mutation_count
  

.. _conf_pmsignature:

6. pmsignature
---------------------------

:doc:`exec_pmsignature` の手順で実行する場合、configファイルの変更は必要ありません。

pmsignatureデータ準備方法およびjsonファイルフォーマットについては :doc:`exec_pmsignature` に記載しています。

.. code-block:: cfg
  :linenos:
  
  ###################### pmsignature
  [pmsignature]

  # ポップアップウィンドウの表示内容
  # 詳細はページ下段の「ユーザ定義フォーマット」に記載
  tooltip_format_ref1 = A: {a:.2}
  tooltip_format_ref2 = C: {c:.2}
  tooltip_format_ref3 = G: {g:.2}
  tooltip_format_ref4 = T: {t:.2}
  tooltip_format_alt1 = C -> A: {ca:.2}
  tooltip_format_alt2 = C -> G: {cg:.2}
  tooltip_format_alt3 = C -> T: {ct:.2}
  tooltip_format_alt4 = T -> A: {ta:.2}
  tooltip_format_alt5 = T -> C: {tc:.2}
  tooltip_format_alt6 = T -> G: {tg:.2}
  tooltip_format_strand = + {plus:.2} - {minus:.2}
  tooltip_format_mutation_title = {id}
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
  # pmsignatureのboxの色
  color_A = #06B838
  color_C = #609CFF
  color_G = #B69D02
  color_T = #F6766D
  color_plus = #00BEC3
  color_minus = #F263E2
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  [result_format_pmsignature]

  # 入力形式 (現在はjsonのみ)
  format = json

  # background を使用しているかどうか
  background = True

  # jsonファイルのkey名
  key_id = id
  key_mutation = mutation
  key_ref = ref
  key_alt = alt
  key_strand = strand
  key_mutation_count = mutation_count


7. 共通項目
---------------

.. _suffix:

suffixとID
====================

paplotではサンプル名が必要です。ファイル入力では、以下のことに注意してください。

 - case1: マージされたファイルを入力する
 
   複数サンプルの結果が、1ファイルにすべてまとめられていると想定しています。サンプル名となる列を ``col_opt_ID`` で必ず指定してください。

 - case2: サンプルごとに分かれた複数のファイルを入力し、データ中にサンプル名となるものはない。
 
   ファイル名の一部をサンプル名として使用します。 ``suffix`` を必ず指定してください。

 - case3: サンプルごとに分かれた複数のファイルを入力し、データ中にサンプル名となるデータがある。
 
   サンプル名となる列を ``col_opt_ID`` で必ず指定してください。

.. image:: image/id_suffix.PNG
  :scale: 100%

複数ファイル入力する場合のコマンドの実行方法は :doc:`command` を参照してください。

.. _data_format:

入力ファイルフォーマット
=========================

configファイル中、[result_format_*] というセクションでは入力ファイルのフォーマットを指定します。

:suffix:  :ref:`suffixとID<suffix>` を参照してください。

:sept: データ区切り。

.. code-block:: cfg

  # タブ区切りの場合
  sept = \t
  
  # ,区切りの場合
  sept = ,
  
  # スペース区切りの場合
  sept = " "

:header: 先頭1行がヘッダかどうか。先頭行がヘッダの場合はTrue。ヘッダなしの場合はFalse

:comment: 先頭に指定文字がある行は飛ばす

出力ファイルフォーマット
=========================

configファイル中、[merge_format_*] というセクションでは出力ファイル(data_*.csv) のフォーマットを指定します。

通常、変更する必要はありません。

:sept: データ区切り。(入力ファイルフォーマットと同)

:lack_column_complement: カラムがない場合、何で埋めるか

.. _column:

列の指定方法
====================

ヘッダの有り無しに合わせて、カラム名もしくはカラムインデックスを入力します。

.. image:: image/col_pos.PNG
  :scale: 100%

記入例

.. code-block:: cfg

  # ヘッダ行がある場合、カラム名 (テキスト) を入力する
  header = True
  col_chr1 = Chr_1
  col_break1 = Pos_1
  col_chr2 = Chr_2
  col_break2 = Pos_2

  # ヘッダ行がない場合、カラムインデックス (数値) を入力する
  header = False
  col_chr1 = 0
  col_break1 = 1
  col_chr2 = 3
  col_break2 = 4

  
.. _user_format:

ユーザ定義フォーマット
=======================

mouse overにより表示するポップアップのようにグラフそのものに影響を与えないような文字列はある程度変更することができます。

表示箇所ごとにそれぞれ設定しますが、書き方は同一です。

設定例

::

  tooltip_format_checker_partial = type[{func}], {chr}:{start}:{end}, [{ref} -----> {alt}]
  
  表示例：
  type[exome], chr1:2000:2001, [A -----> T]

{}で囲った文字がキーワードで、実際の値に置き換えられます。
キーワードとはconfigファイルで各データ列を設定した項目のうち、``col_`` もしくは ``col_opt_`` を除いた名前です。
大文字と小文字の区別はありません。
たとえば、CHR, Chr, chr はすべて同一とみなしますので、ご注意ください。

デフォルトで設定しているのは下記ですが、任意で増やすことができます。
その場合は、```col_opt_{任意の名前}``` として追加し、実際のデータの列名を指定してください。

``col_opt_new_option = column_name``

記載方法詳細は各項目参照

 - :doc:`config_mat` 
 - :doc:`config_ca` 
 - :doc:`config_qc` 
 - :doc:`config_signature` 
 - :doc:`config_pmsignature` 

::

  数値計算させることもできます。その場合、計算式を{}で囲います。
  
  {#number_mutaion_gene/#number_id*100}%
  
  表示例：
  3.33333333333333%
  
  表示桁数を指定したい場合は計算式の後に ":.2" と書きます。小数点以下3桁の場合は ":.3" と書きます。
  
  {#number_mutaion_gene/#number_id*100:.2}%
  
  表示例：
  3.33%

.. |new| image:: image/tab_001.gif
