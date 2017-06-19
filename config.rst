*******************************
Config 全設定項目
*******************************

.. _conf_mm:

=======================
1. mutation-matrix
=======================

----------------------------------------------------------
全設定項目
----------------------------------------------------------

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

----------------------------------------------------------
ポップアップウィンドウの表示内容
----------------------------------------------------------

| 記載方法は :ref:`ユーザ定義フォーマット<user_format>` を参照してください。
| 
| 表示箇所ごとに6種類設定しますが、書き方は同一です。
| データ列とは別に以下も特殊キーワードとして使用することができます。
|

:{#number_id}:      サンプル数
:{#number_gene}:    遺伝子数
:{#number_mutaion}: mutation数(同一サンプルが同一遺伝子で複数回検出されても1としてカウントする)
:{#sum_mutaion}:    mutation総検出数
:{#item_value}:     積み上げグラフの1項目の値
:{#sum_item_value}: 積み上げグラフの合計値

| mutationの集計について、使用しなかったmutationはカウントしていません。
|

**デフォルトでの設定内容と表示との対応**

.. code-block:: cfg

  # グリッド - タイトル
  tooltip_format_checker_title1 = ID:{ID}, gene:{gene}, {#sum_item_value}
  
  # グリッド - funcごと
  tooltip_format_checker_partial = type[{func}], {chr}:{start}:{end}, [{ref} -----> {alt}]
  
  # 遺伝子グラフ - タイトル
  tooltip_format_gene_title = gene:{gene}, {#sum_item_value}
  
  # 遺伝子グラフ - funcごと
  tooltip_format_gene_partial = func:{func}, {#item_value}
  
  # サンプルグラフ - タイトル
  tooltip_format_id_title = ID:{id}, {#sum_item_value}
  
  # サンプルグラフ - funcごと
  tooltip_format_id_partial = func:{func}, {#item_value}

.. image:: image/conf_mut4.PNG
  :scale: 100%

=======================
2. QC
=======================

全設定項目
---------------------------------

.. code-block:: cfg
  
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

=======================
3. CA
=======================

全設定項目
---------------------------------

.. code-block:: cfg
  
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

=======================
4. signature |new|
=======================

----------------------------------------------------------
全設定項目
----------------------------------------------------------

.. code-block:: cfg
  
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

----------------------------------------------------------
ポップアップウィンドウの表示内容
----------------------------------------------------------

| 記載方法は :ref:`ユーザ定義フォーマット<user_format>` を参照してください。
| 
| 表示箇所ごとに4種類設定しますが、書き方は同一です。
| それぞれ次のキーワードが使用できます。
|

**tooltip_format_signature_title**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{sig}              signatureの色別グループのラベル。'C > A' や 'C > G' 等
{#sum_group_value} signatureの色別グループの合計値
================== ============================================================

**tooltip_format_signature_partial**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{route}            signatureの棒グラフ1本分のラベル。'ApCpA' や 'CpCpA' 等
{#sum_item_value}  signatureの棒グラフ1本分の値
================== ============================================================

**tooltip_format_mutation_title (積み上げグラフ)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{id}               `key_id` で入力したサンプル名です。
{#sum_mutaion_all} 全mutation数
================== ============================================================

**tooltip_format_mutation_partial (積み上げグラフ)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{sig}              signature名 "Signature {signature番号}" で表示します。
{#sum_item_value}  積み上げグラフの合計値
================== ============================================================


**デフォルトでの設定内容と表示との対応**

.. code-block:: cfg

  # signature - タイトル
  tooltip_format_signature_title = {sig}
  
  # signature - 各項目
  tooltip_format_signature_partial = {route}: {#sum_item_value:6.2}
  
  # 積み上げグラフ - タイトル
  tooltip_format_mutation_title = {id}
  
  # 積み上げグラフ - signatureごと
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
.. image:: image/conf_sig1.PNG
  :scale: 100%

=======================
5. pmsignature |new|
=======================

----------------------------------------------------------
全設定項目
----------------------------------------------------------

.. code-block:: cfg
  
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
  
----------------------------------------------------------
ポップアップウィンドウの表示内容
----------------------------------------------------------

| 記載方法は :ref:`ユーザ定義フォーマット<user_format>` を参照してください。
| 
| 表示箇所ごとに4種類設定しますが、書き方は同一です。
| それぞれ次のキーワードが使用できます。
|

**tooltip_format_ref* (pmsignature 下段の5つのbox)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{a}                Aの値
{c}                Cの値
{g}                Gの値
{t}                Tの値
================== ============================================================

**tooltip_format_alt* (pmsignature 上段の1つのbox)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{ca}               C->Aの値
{cg}               C->Gの値
{ct}               C->Tの値
{ta}               T->Aの値
{tc}               T->Cの値
{tg}               T->Gの値
================== ============================================================

**tooltip_format_strand**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{plus}             プラスの値
{minus}            マイナスの値
================== ============================================================

**tooltip_format_mutation_title (積み上げグラフ)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{id}               `key_id` で入力したサンプル名です。
{#sum_mutaion_all} 全mutation数
================== ============================================================

**tooltip_format_mutation_partial (積み上げグラフ)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{sig}              signature名 "Signature {signature番号}" で表示します。
{#sum_item_value}  積み上げグラフの合計値
================== ============================================================

**デフォルトでの設定内容と表示との対応**

.. code-block:: cfg

  # pmsignature - 下段の5つのbox
  tooltip_format_ref1 = A: {a:.2}
  tooltip_format_ref2 = C: {c:.2}
  tooltip_format_ref3 = G: {g:.2}
  tooltip_format_ref4 = T: {t:.2}

  # pmsignature - 上段のbox
  tooltip_format_alt1 = C -> A: {ca:.2}
  tooltip_format_alt2 = C -> G: {cg:.2}
  tooltip_format_alt3 = C -> T: {ct:.2}
  tooltip_format_alt4 = T -> A: {ta:.2}
  tooltip_format_alt5 = T -> C: {tc:.2}
  tooltip_format_alt6 = T -> G: {tg:.2}

  # pmsignature - strand
  tooltip_format_strand = + {plus:.2} - {minus:.2}
  
  # 積み上げグラフ - タイトル
  tooltip_format_mutation_title = {id}
  
  # 積み上げグラフ - signatureごと
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
.. image:: image/conf_pmsig1.PNG
  :scale: 100%

.. |new| image:: image/tab_001.gif
