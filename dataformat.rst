**************************
データフォーマット
**************************

ここでは、exampleデータ (※) を基にして、それぞれのレポートを出力するために必要な入力データを解説します。

※ exampleデータはpaplotをダウンロードして解凍したディレクトリ中、exampleディレクトリにあります。

.. _conf_mm:

----------------------
1. mutation-matrix
----------------------

==========================
最小データセット
==========================

| `view report <http://genomon-project.github.io/paplot/mutation/graph_minimal.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_minimal>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_minimal.zip?raw=true>`_ 

paplotでmutation-matrixを作成するために最低限必要な項目はサンプルID(ID)、gene名(gene)、変異タイプ(func) の3つです。

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_minimal/data.csv
  
  ID,func,gene
  SAMPLE00,intronic,GATA3
  SAMPLE00,UTR3,CDH1
  SAMPLE00,exonic,GATA3
  SAMPLE01,splicing,WASF3
  SAMPLE01,intronic,WASF3
  SAMPLE01,exonic,NRAS
  SAMPLE02,intronic,FBXW7
  SAMPLE02,intronic,GATA3
  SAMPLE02,ncRNA_intronic,ACVR2B
  SAMPLE03,exonic,CAP2
  SAMPLE03,intronic,PIK3CA
  SAMPLE03,downstream,SEPT12

configファイルの[result_format_mutation]セクションでデータの列名を以下のように設定します。

.. code-block:: cfg
  :caption: example/mutation_minimal/paplot.cfg

  [result_format_mutation]
  # column index (required)
  col_func = func
  col_gene = gene
  
  # column index (option)
  col_opt_id = ID


編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_minimal/data.csv ./tmp mutation_minimal \
  --config_file {unzip_path}/example/mutation_minimal/paplot.cfg

----

==========================
タブ区切り
==========================

データファイルがタブ区切りであった場合、以下のように設定します。

.. code-block:: cfg
  
  [result_format_mutation]
  sept = \t

----

==========================
ヘッダなし
==========================

| `view report <http://genomon-project.github.io/paplot/mutation/graph_noheader.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_noheader>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_noheader.zip?raw=true>`_ 

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_noheader/data.csv

  SAMPLE00,intronic,GATA3
  SAMPLE00,UTR3,CDH1
  SAMPLE00,exonic,GATA3
  SAMPLE01,splicing,WASF3
  SAMPLE01,intronic,WASF3
  SAMPLE01,exonic,NRAS
  SAMPLE02,intronic,FBXW7
  SAMPLE02,intronic,GATA3
  SAMPLE02,ncRNA_intronic,ACVR2B
  SAMPLE03,exonic,CAP2
  SAMPLE03,intronic,PIK3CA
  SAMPLE03,downstream,SEPT12

データにヘッダ行がない場合、列名でなく列番号を設定します。

configファイルの[result_format_mutation]セクションでデータの列番号を以下のように設定します。

列番号は左から順に1始まりで数えます。

.. code-block:: cfg
  :caption: example/mutation_noheader/paplot.cfg
  
  [result_format_mutation]
  # column index (required)
  col_func = 2
  col_gene = 3
  
  # column index (option)
  col_opt_id = 1

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_noheader/data.csv ./tmp mutation_noheader \
  --config_file {unzip_path}/example/mutation_noheader/paplot.cfg

----

==========================
ポップアップの情報追加
==========================

| `view report <http://genomon-project.github.io/paplot/mutation/graph_option.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_option>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_option.zip?raw=true>`_ 

マウスオーバーで表示する情報をカスタマイズすることができます。

最小構成で表示するポップアップ（グリッド部分）はこのようになっています。

.. image:: image/data_mut1.png

ここに情報を追加してポジションや変異内容を確認できるように変更します。

変更後

.. image:: image/data_mut2.png

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_option/data.csv
  
  ID,Chr,Start,End,Ref,Alt,func,gene
  SAMPLE00,chr10,8114472,8114474,A,C,intronic,GATA3
  SAMPLE00,chr13,28644892,28644901,G,-,intronic,FLT3
  SAMPLE00,chr13,28664636,28664638,-,G,intronic,FLT3
  SAMPLE00,chr16,68795521,68795530,-,T,UTR3,CDH1
  SAMPLE00,chr10,8117068,8117069,G,T,exonic,GATA3
  SAMPLE00,chr3,178906688,178906688,G,A,intronic,PIK3CA
  SAMPLE00,chr13,28603715,28603715,G,-,intergenic,FLT3
  SAMPLE00,chr14,103368263,103368270,G,C,intronic,TRAF3
  SAMPLE00,chr1,26505548,26505557,T,C,exonic,CNKSR1
  SAMPLE00,chr7,140619975,140619979,-,G,intronic,BRAF
  SAMPLE00,chr14,103320225,103320225,-,T,downstream,TRAF3

今回の例では、必須項目であるサンプルID(ID)、gene名(gene)、変異タイプ(func) に加えて、
Chromosome(Chr), 変異開始位置(Start),変異終了位置(End), リファレンスの塩基 (Ref), 変異の塩基(Alt)を追加しています。

まず、追加した列名をconfigファイルに記載します。

configファイルの[result_format_mutation]セクションでデータの列名を以下のように設定します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [result_format_mutation]
  # column index (option)
  col_opt_chr = Chr
  col_opt_start = Start
  col_opt_end = End
  col_opt_ref = Ref
  col_opt_alt = Alt

オプションの列名は ``col_opt_{name} = {columun name}`` というように記述します。

``{name}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。

次に、ポップアップの表示内容を変更します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [mutation]
  # 最小構成での設定
  # tooltip_format_checker_partial = type[{func}]
  # 次のように変更
  tooltip_format_checker_partial = type[{func}], {chr}:{start}:{end}, [{ref} -----> {alt}]

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_option/data.csv ./tmp mutation_option \
  --config_file {unzip_path}/example/mutation_option/paplot.cfg

----

=============================================
サブプロットとしてクリニカルデータを追加
=============================================

| `view report <http://genomon-project.github.io/paplot/mutation/graph_subplot.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_subplot>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_subplot.zip?raw=true>`_ 

変異以外のサンプルに関する情報（例えばクリニカルデータ）をサブプロットとしてmutation-matrixに追加することができます。

.. image:: image/data_mut3.png

exampleでは別ファイルとして以下のデータファイルを用意しています。

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_subplot/data_subplot.csv
  
  ID,gender,age,BMI
  SAMPLE00,F,30,40
  SAMPLE01,F,62,25
  SAMPLE02,F,59,34
  SAMPLE03,M,66,26
  SAMPLE04,M,53,40
  SAMPLE05,F,79,27
  SAMPLE06,M,64,29
  SAMPLE07,M,54,22
  SAMPLE08,F,55,35

今回の例では、サンプルID(ID)、gender、age、BMIを用意していますが、そのうち、必須項目はサンプルID(ID)です。
データファイル中のサンプルIDと紐づけられることが重要です。

configファイルにサブプロットの設定を追加します。

configファイルに[mutation_subplot_type1_1]セクションを追加し、以下のように設定します。

.. code-block:: cfg
  :caption: example/mutation_subplot/paplot.cfg
  
  ### sample for subplot
  [mutation_subplot_type1_1]

  # サブプロットのタイトル
  title = Clinical Gender

  # サブプロットのデータファイルのパスを設定します
  path = {unzip_path}/example/mutation_subplot/data_subplot.csv

  # データ区切り
  sept = ,

  # ヘッダ有り無し（ない場合はFalse)
  header = True

  # コメント行の先頭文字
  comment = 

  # 列名（ヘッダがない場合は列番号）
  col_value = gender

  # サンプルIDの列名（ヘッダがない場合は列番号）
  col_id = ID
  
  # 表示形式 (欄外参照)
  # fix, range, gradientから選択
  mode = fix
  
  # サブプロットの色と凡例 (欄外参照)
  name_set = M:Male:blue, F:Female:red


サブプロットの表示位置
--------------------------

mutation-matrixグラフでは解析結果とは別にサンプルに対する情報を表示することができます。

表示場所は2つあり、type1はサンプルグラフの下に、type2は最後に表示します。

type1を表示する場合はセクション名を[mut_subplot_type1_*]とします。

type2を表示する場合はセクション名を[mut_subplot_type2_*]とします。

``*`` には1から始まる連番を入れてください。1から順に表示します。

サブプロットの表示形式
--------------------------

表示形式 (mode) は3種類あり、fix, range, gradientから選択します。

.. image:: image/conf_mut3.PNG
  :scale: 100%

name_setの書き方
-----------------------

サブプロットの色と判例を定義します。

``{値}:{表示文字列}:{セルの色}`` を各値ごとに記入します。セルの色は省略可能です。

mode = fixの場合

.. code-block:: cfg
  
  name_set = 0:Male:blue, 1:Female:red, 2:Unknown:gray

mode = rangeの場合

値には範囲開始の値を記入します。

.. code-block:: cfg
  
  name_set = 0:0-19, 20:20-39, 40:40-59, 60:60over

mode = gradientの場合

最初と最後の値を記入します。MIN/MAXを使用すると、データから自動的に設定します。

.. code-block:: cfg

  # 自動設定の場合
  name_set = MIN:min, MAX:max

  # 手動設定の場合
  name_set = 0:min (0), 40:max (40)
  

titleとnameset
--------------------------

.. image:: image/conf_mut2.PNG
  :scale: 100%

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_subplot/data.csv ./tmp mutation_subplot \
  --config_file {unzip_path}/example/mutation_subplot/paplot.cfg

----

.. _conf_qc:

------------
2. QC
------------

==========================
最小データセット
==========================

| `view report <http://genomon-project.github.io/paplot/qc/graph_minimal.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_minimal>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_minimal.zip?raw=true>`_ 

paplotでQCレポートを作成するために最低限必要な情報はサンプルID(ID)とQCの値（最低1項目）です。

今回の例では、depth-averageを使用していますが、ほかの値でも問題ありません。

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/qc_minimal/data.csv
  
  ID,average_depth
  SAMPLE1,70.0474
  SAMPLE2,65.7578
  SAMPLE3,63.3750
  SAMPLE4,70.9654
  SAMPLE5,69.9653

まず、configファイルの[result_format_qc]セクションに入力データの列名を登録します。

.. code-block:: cfg
  :caption: example/qc_minimal/paplot.cfg
  
  [result_format_qc]
  # column index (option)
  col_opt_average_depth = average_depth
  col_opt_id = ID

オプションの列名は ``col_opt_{name} = {columun name}`` というように記述します。

``{name}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。

次に、configファイルに[qc_chart_1]セクションを追加し、以下のように設定します。

.. code-block:: cfg
  :caption: example/qc_minimal/paplot.cfg
  
  [qc_chart_1]
  
  # グラフのタイトル
  title = depth average
  
  # Y軸のラベル
  title_y = average of depth
  
  # 積み上げ要素（今回は1項目のみなので、通常の棒グラフとなる）
  stack1 = {average_depth}
  
  # グラフの色と凡例 (欄外参照)
  name_set = average_depth:#2478B4
  
  # マウスオーバーで表示する情報のフォーマット
  tooltip_format1 = ID:{id}
  tooltip_format2 = {average_depth:.2}

ここで、 ``average_depth`` という値を変数のとして使用していますが、これは [result_format_qc]セクションで指定した ``col_opt_average_depth`` 項目のうち、``col_opt_`` を除いた名前です。

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_minimal/data.csv ./tmp qc_minimal \
  --config_file {unzip_path}/example/qc_minimal/paplot.cfg

----

==========================
タブ区切り
==========================

データファイルがタブ区切りであった場合、以下のように設定します。

.. code-block:: cfg
  
  [result_format_qc]
  sept = \t

----

==========================
ヘッダなし
==========================

| `view report <http://genomon-project.github.io/paplot/qc/graph_noheader.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_noheader>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_noheader.zip?raw=true>`_ 

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/qc_noheader/data.csv
  
  SAMPLE1,70.0474
  SAMPLE2,65.7578
  SAMPLE3,63.3750
  SAMPLE4,70.9654
  SAMPLE5,69.9653

データにヘッダ行がない場合、列名でなく列番号を設定します。

configファイルの[result_format_qc]セクションでデータの列番号を以下のように設定します。

列番号は左から順に1始まりで数えます。

.. code-block:: cfg
  :caption: example/qc_noheader/paplot.cfg
  
  [result_format_qc]
  col_opt_average_depth = 2
  col_opt_id = 1

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_noheader/data.csv ./tmp qc_noheader \
  --config_file {unzip_path}/example/qc_noheader/paplot.cfg

----

==========================
複数グラフ
==========================

| `view report <http://genomon-project.github.io/paplot/qc/graph_multi_plot.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_multi_plot>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_multi_plot.zip?raw=true>`_ 

最小構成では1つのグラフを作成しました。今回は複数のグラフを作成します。

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/qc_multi_plot/data.csv
  
  ID,average_depth,read_length_r1,read_length_r2,total_reads,mapped_reads,mean_insert_size,duplicate_reads,2x_rt,10x_rt,20x_rt,30x_rt
  SAMPLE1,70.0474,265,270,94315157,56262203,343.92,7964009,0.9796,0.7680,0.6844,0.6747
  SAMPLE2,65.7578,140,200,50340277,33860998,351.23,5297450,0.8489,0.7725,0.7655,0.6131
  SAMPLE3,63.3750,120,175,90635480,88010999,496.34,8347508,0.9814,0.8236,0.6045,0.5889
  SAMPLE4,70.9654,120,140,72885114,89163960,696.23,6726021,0.9047,0.8303,0.7032,0.6801
  SAMPLE5,69.9653,230,110,92572101,28793615,731.98,9794813,0.9776,0.9452,0.6720,0.6518

ここでは以下の構成でグラフを作成します。

 - chart_1　[棒グラフ] average_depth
 - chart_2　[積み上げグラフ] 2x_rt,10x_rt,20x_rt,30x_rt
 - chart_3　[棒グラフ] mapped_readsをtotal_readsで割る
 - chart_4　[棒グラフ] mean_insert_size
 - chart_5　[棒グラフ] duplicate_readsをtotal_readsで割る
 - chart_6　[積み上げグラフ] read_length_r1,read_length_r2

完成したグラフはここ `view <http://genomon-project.github.io/paplot/qc/graph_multi_plot.html>`_ を参照してください。

まず、configファイルの[result_format_qc]セクションに入力データの列名を登録します。

.. code-block:: cfg
  :caption: example/qc_multi_plot/paplot.cfg
  
  [result_format_qc]
  # column index (option)
  col_opt_average_depth = average_depth
  col_opt_id = ID
  col_opt_duplicate_reads = duplicate_reads
  col_opt_mapped_reads = mapped_reads
  col_opt_total_reads = total_reads
  col_opt_mean_insert_size = mean_insert_size
  col_opt_ratio_2x = 2x_rt
  col_opt_ratio_10x = 10x_rt
  col_opt_ratio_20x = 20x_rt
  col_opt_ratio_30x = 30x_rt
  col_opt_read_length_r1 = read_length_r1
  col_opt_read_length_r2 = read_length_r2

オプションの列名は ``col_opt_{name} = {columun name}`` というように記述します。

``{name}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。

次に、configファイルに[qc_chart_1],[qc_chart_2],[qc_chart_3]... セクションを追加し、順番に設定します。

| QCレポートは[qc_chart_1],[qc_chart_2],[qc_chart_3] の順番に表示し、必要な数だけ [qc_chart_*] セクションを増やすことができます。
| ``*`` には1から始まる連番を入れてください。1から順に表示します。

ここでは各設定について解説します。

完成したconfigファイルはここ `config <https://github.com/Genomon-Project/paplot/blob/master/example/qc_multi_plot/paplot.cfg>`_ を参照してください。

chart_1 (average_depth) と chart_4 (mean_insert_size) は単純な棒グラフです。

記載方法は最小構成と同じですので、ここでは割愛します。

列同士の数値演算
-----------------------

chart_3 (mapped_reads) と chart_5 (duplicate_reads) は列同士で計算（今回は割り算）させて出力します。

.. code-block:: cfg
  :caption: example/qc_multi_plot/paplot.cfg

  [qc_chart_3]
  
  # 表示する文字列を設定します
  title = mapped_reads/total_reads
  title_y = rate
  
  # 凡例の文字列と色を設定します
  name_set = mapped_reads/total_reads:#2478B4
  
  # グラフの値
  stack1 = {mapped_reads/total_reads}
  
  # ポップアップの表示内容
  tooltip_format1 = ID:{id}
  tooltip_format2 = {mapped_reads/total_reads:.2}

上記では、 ``stack1 = {mapped_reads/total_reads}`` として記入しています。

ここで ``{mapped_reads/total_reads}`` と書くと割り算に、 ``{mapped_reads+total_reads}`` と書くと足し算させることができます。

tooltip_format2でも同様に数値演算させています。

tooltip_format2 = {mapped_reads/total_reads:.2}

このように書くと、mapped_readsをtotal_readsで割ったものを小数点第2位まで表示する、という意味になります。

積み上げグラフ　その１
-----------------------

chart_6 (read_length_r1,read_length_r2) は積み上げグラフです。

.. code-block:: cfg
  :caption: example/qc_multi_plot/paplot.cfg
  
  [qc_chart_6]
  
  # 表示する文字列を設定します
  title = read_length_r1, read_length_r2
  title_y = read_length

  # 凡例の文字列と色を設定します
  name_set = read_length_r1:#2478B4, read_length_r2:#FF7F0E
  
  # グラフの値
  stack1 = {read_length_r1}
  stack2 = {read_length_r2}
  
  # ポップアップの表示内容
  tooltip_format1 = ID:{id}
  tooltip_format2 = r1: {read_length_r1: ,}
  tooltip_format3 = r2: {read_length_r2: ,}

上記では、 stack1にread_length_r1を、stack2にread_length_r2を記入しています。

1，2，3の順に下から表示します。1を一番下に表示します。


積み上げグラフ　その２
-----------------------

chart_6 (2x_rt,10x_rt,20x_rt,30x_rt) は積み上げグラフですが数値演算もしています。

.. code-block:: cfg
  :caption: example/qc_multi_plot/paplot.cfg
  
  [qc_chart_2]
  
  # 表示する文字列を設定します
  title = depth coverage
  title_y = coverage
  
  # 凡例の文字列と色を設定します
  name_set = ratio_30x:#2478B4, ratio_20x:#FF7F0E, ratio_10x:#2CA02C, ratio_2x:#D62728
  
  # グラフの値
  stack1 = {ratio_30x}
  stack2 = {ratio_20x-ratio_30x}
  stack3 = {ratio_10x-ratio_20x}
  stack4 = {ratio_2x-ratio_10x}
  
  # ポップアップの表示内容
  tooltip_format1 = ID:{id}
  tooltip_format2 = ratio__2x: {ratio_2x:.2}
  tooltip_format3 = ratio_10x: {ratio_10x:.2}
  tooltip_format4 = ratio_20x: {ratio_20x:.2}
  tooltip_format5 = ratio_30x: {ratio_30x:.2}

上記では、 stack1にratio_30xを、stack2にratio_20xからratio_30xを引いたものを表示ししています。

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_multi_plot/data.csv ./tmp qc_multi_plot \
  --config_file {unzip_path}/example/qc_multi_plot/paplot.cfg

----

==========================
データ選択
==========================

| `view report <http://genomon-project.github.io/paplot/qc/graph_brush.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_brush>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_brush.zip?raw=true>`_ 

前章で作成した複数のグラフに対し、領域選択用のグラフを追加します。

完成したグラフはここ `view <http://genomon-project.github.io/paplot/qc/graph_brush.html>`_ を参照してください。

データ列はaverage_depthを使用します。

もし、新しいデータ列を使用する場合は設定ファイルの[result_format_qc]セクションにcol_opt_{name} として登録してください。

領域選択用のグラフは[qc_chart_brush]というセクション名で一つだけ追加することができます。

.. code-block:: cfg
  :caption: example/qc_brush/paplot.cfg
  
  [qc_chart_brush]
  stack = {average_depth}
  name_set = average:#E3E5E9

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_brush/data.csv ./tmp qc_brush \
  --config_file {unzip_path}/example/qc_brush/paplot.cfg

----

.. _conf_ca:

--------------
3. CA
--------------

==========================
最小データセット
==========================

| `view report <http://genomon-project.github.io/paplot/ca/graph_minimal.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_minimal>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_minimal.zip?raw=true>`_ 

paplotでcaレポートを作成するために最低限必要な項目はサンプルID(ID)、ブレークポイント1のchromosome (Chr1) とposition(Break1)、ブレークポイント2のchromosome (Chr2) とposition(Break2) の5つです。

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_minimal/data.csv
  
  ID,Chr1,Break1,Chr2,Break2,
  SAMPLE1,14,16019088,12,62784483,
  SAMPLE1,9,99412502,7,129302434,
  SAMPLE1,13,84663781,18,52991509,
  SAMPLE2,11,101374238,22,26701405,
  SAMPLE2,2,121708638,7,137424167,
  SAMPLE3,22,34268355,10,19871820,
  SAMPLE3,8,107868940,hs37d5,20517614,
  SAMPLE4,8,135644313,3,116748248,
  SAMPLE4,7,6037836,21,34855497,
  SAMPLE4,7,109724564,14,106387943,

configファイルの[result_format_mutation]セクションでデータの列名を以下のように設定します。

``example/ca_minimal/paplot.cfg``

.. code-block:: cfg

  [result_format_ca]
  # column index (required)
  col_chr1 = Chr1
  col_break1 = Break1
  col_chr2 = Chr2
  col_break2 = Break2
  
  # column index (option)
  col_opt_id = ID

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot ca {unzip_path}/example/ca_minimal/data.csv ./tmp ca_minimal \
  --config_file {unzip_path}/example/ca_minimal/paplot.cfg

----

==========================
タブ区切り
==========================

データファイルがタブ区切りであった場合、以下のように設定します。

.. code-block:: cfg
  
  [result_format_ca]
  sept = \t

----

==========================
ヘッダなし
==========================

| `view report <http://genomon-project.github.io/paplot/ca/graph_noheader.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_noheader>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_noheader.zip?raw=true>`_ 

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/ca_noheader/data.csv
  
  SAMPLE00,intronic,GATA3
  SAMPLE00,UTR3,CDH1
  SAMPLE00,exonic,GATA3
  SAMPLE01,splicing,WASF3
  SAMPLE01,intronic,WASF3
  SAMPLE01,exonic,NRAS
  SAMPLE02,intronic,FBXW7
  SAMPLE02,intronic,GATA3
  SAMPLE02,ncRNA_intronic,ACVR2B
  SAMPLE03,exonic,CAP2
  SAMPLE03,intronic,PIK3CA
  SAMPLE03,downstream,SEPT12

データにヘッダ行がない場合、列名でなく列番号を設定します。

configファイルの[result_format_ca]セクションでデータの列番号を以下のように設定します。

列番号は左から順に1始まりで数えます。

.. code-block:: cfg
  :caption: example/ca_noheader/paplot.cfg
  
  # column index (required)
  col_chr1 = 2
  col_break1 = 3
  col_chr2 = 4
  col_break2 = 5
  
  # column index (option)
  col_opt_id = 1

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot ca {unzip_path}/example/ca_noheader/data.csv ./tmp ca_noheader \
  --config_file {unzip_path}/example/ca_noheader/paplot.cfg

----

==========================
変異のグルーピング
==========================

| `view report <http://genomon-project.github.io/paplot/ca/graph_group.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_group>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_group.zip?raw=true>`_ 

最小構成で作成した変異には自動的にグループ機能が働いており、クロモソーム内の変異（緑）とクロモソーム間の変異（紫）に色分けされています。

ここでは、グループを手動で設定するように変更します。

データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_option/data.csv
  
  ID,Chr1,Break1,Chr2,Break2,type
  SAMPLE1,14,16019088,12,62784483,C
  SAMPLE1,9,99412502,7,129302434,B
  SAMPLE1,13,84663781,18,52991509,A
  SAMPLE2,11,101374238,22,26701405,B
  SAMPLE2,2,121708638,7,137424167,C
  SAMPLE2,16,43027789,22,23791492,C
  SAMPLE3,22,34268355,10,19871820,A
  SAMPLE3,14,56600342,hs37d5,5744957,B
  SAMPLE3,Y,12191863,hs37d5,29189687,A
  SAMPLE4,8,135644313,3,116748248,D
  SAMPLE4,7,6037836,21,34855497,D
  SAMPLE4,7,109724564,14,106387943,A

今回の例では、必須項目であるID、Chr1、Break1、Chr2、Break2 に加えて、type が追加してあります。

まず、グルーピングに使用する列名、type をconfigファイルに記載します。

configファイルの[result_format_mutation]セクションでデータの列名を以下のように設定します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [result_format_ca]
  col_opt_group = type

オプションの列名は通常任意に設定できますが、グルーピングにおいては ``col_opt_group`` 固定にしてください。

これで ``type`` 列を使用してグルーピングされますが、追加で色も指定できます。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg

  [ca]
  # グループの色指定
  group_colors = A:#66C2A5,B:#FC8D62,C:#8DA0CB,D:#E78AC3

  # 指定したグループのみ表示する
  limited_group = 
  
  # 指定したグループを表示しない
  nouse_group = 


編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot ca {unzip_path}/example/ca_group/data.csv ./tmp ca_group \
  --config_file {unzip_path}/example/ca_group/paplot.cfg

----

==========================
ポップアップの情報追加
==========================

| `view report <http://genomon-project.github.io/paplot/ca/graph_option.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_option>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/ca_option.zip?raw=true>`_ 

マウスオーバーで表示する情報をカスタマイズすることができます。

最小構成で表示するポップアップはこのようになっています。

.. image:: image/data_ca1.png

ここにもう少し情報を追加して変異の詳細を確認できるように変更します。

変更後

.. image:: image/data_ca2.png


データファイルから一部抜粋

.. code-block:: cfg
  :caption: example/mutation_option/data.csv
  
  ID,Chr1,Break1,Dir1,Chr2,Break2,Dir2,Ref,Alt,func,gene1,gene2
  SAMPLE1,14,16019088,-,12,62784483,+,---,GACTC,deletion,LS7T1EG444,4GRRIO5AVR
  SAMPLE1,9,99412502,-,7,129302434,+,---,C-CT-,translocation,FQFW16UF5U,QP779MLPNV
  SAMPLE1,13,84663781,+,18,52991509,-,---,GTAAA,deletion,Q9VX1I9U3I,7XM09ETN40
  SAMPLE2,11,101374238,+,22,26701405,+,---,TGGGT,translocation,FZ7LOS66RD,9WYBJR57E0
  SAMPLE2,2,121708638,-,7,137424167,-,---,G-TGA,translocation,5655M5E46B,HB14VJXDHV
  SAMPLE2,16,43027789,+,22,23791492,-,---,CCTCA,inversion,REFSIL0H2M,L5EA31R8U0
  SAMPLE3,22,34268355,+,10,19871820,+,---,TC-GT,tandem_duplication,9SVRQCFVCO,2BEWSO91FZ
  SAMPLE3,14,56600342,-,hs37d5,5744957,+,---,--CAA,deletion,UTLVCZ63SK,5I74M5NKDC
  SAMPLE3,Y,12191863,-,hs37d5,29189687,-,---,TG-G-,inversion,3PLD4C20IZ,BVYMBTIFKD

今回の例では、必須項目であるID、Chr1、Break1、Chr2、Break2 に加えて、
リファレンスの塩基 (Ref), 変異の塩基(Alt), 変異タイプ(func), 遺伝子名(gene1, gene2) Direction(Dir1, Dir2) が追加してあります。

まず、ポップアップの情報として追加したい列名、変異タイプ(func)と 遺伝子名(gene1, gene2)をconfigファイルに記載します。

configファイルの[result_format_mutation]セクションでデータの列名を以下のように設定します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [result_format_ca]
  col_opt_dir1 = Dir1
  col_opt_dir2 = Dir2
  col_opt_type = func
  col_opt_gene_name1 = gene1
  col_opt_gene_name2 = gene2

オプションの列名は ``col_opt_{name} = {columun name}`` というように記述します。

``{name}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。

次に、ポップアップの表示内容を変更します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [ca]
  # 最小構成での設定
  # tooltip_format = [{chr1}] {break1:,}; [{chr2}] {break2:,}
  # 次のように変更
  tooltip_format = [{chr1}] {break1:,} ({dir1}) {gene_name1}; [{chr2}] {break2:,} ({dir2}) {gene_name2}; {type}

編集したconfigファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot ca {unzip_path}/example/ca_option/data.csv ./tmp ca_option \
  --config_file {unzip_path}/example/ca_option/paplot.cfg

.. _conf_signature:

---------------------------
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

---------------------------
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

---------------
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

------------
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



.. |new| image:: image/tab_001.gif
