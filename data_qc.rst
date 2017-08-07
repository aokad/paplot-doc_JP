**************************
QC レポート
**************************

ここでは、サンプルデータ (※) を基にして、QC レポートを出力するために必要な入力データを解説します。

※ サンプルデータはpaplotをダウンロードして解凍したディレクトリ中、exampleディレクトリにあります。

.. _qc_minimal:

==========================
1. 最小データセット
==========================

| `view report <http://genomon-project.github.io/paplot/qc/graph_minimal.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_minimal>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_minimal.zip?raw=true>`_ 

paplotで QC レポートを作成するために最低限必要な情報はサンプルID(ID)と QC の値（最低1項目）です。

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

まず、設定ファイルの [result_format_qc] セクションに入力データの列名を登録します。

.. code-block:: cfg
  :caption: example/qc_minimal/paplot.cfg
  
  [result_format_qc]
  # column index (option)
  col_opt_average_depth = average_depth
  col_opt_id = ID

オプションの列名は次の形式で記述します。 ``col_opt_{name} = {columun name}`` 

``{name}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。

次に、設定ファイルに [qc_chart_1] セクションを追加し、次のように設定します。

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

ここで、 ``average_depth`` という値を変数のように使用していますが、これは [result_format_qc] セクションで指定した ``col_opt_average_depth`` 項目のうち、``col_opt_`` を除いた名前です。

編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_minimal/data.csv ./tmp qc_minimal \
  --config_file {unzip_path}/example/qc_minimal/paplot.cfg


1-1. name_setの書き方
------------------------------

凡例名と色を定義します。

``{要素の凡例名}:{セルの色}`` を積み上げ要素ごとに記入します。セルの色は省略可能です。

.. code-block:: cfg
  
  name_set = average_depth:#2478B4
  
  # 複数ある場合は,で区切って書きます。
  name_set = ratio_30x:#2478B4, ratio_20x:#FF7F0E, ratio_10x:#2CA02C, ratio_2x:#D62728
  
セルの色を省略した場合、以下の色を上から順に使用します。

.. image:: image/default_color.PNG
  :scale: 100%

----

.. _qc_noheader:

==========================
2. ヘッダなし
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

設定ファイルの [result_format_qc] セクションでデータの列番号を次のように設定します。

列番号は左から順に1始まりで数えます。

.. code-block:: cfg
  :caption: example/qc_noheader/paplot.cfg
  
  [result_format_qc]
  col_opt_average_depth = 2
  col_opt_id = 1

編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_noheader/data.csv ./tmp qc_noheader \
  --config_file {unzip_path}/example/qc_noheader/paplot.cfg

----

.. _qc_mplot:

==========================
3. 複数グラフ
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

 - chart_1　[棒グラフ] average_depth (最小構成と同じ)
 - chart_2　[積み上げグラフ] 2x_rt,10x_rt,20x_rt,30x_rt
 - chart_3　[棒グラフ] mapped_readsをtotal_readsで割る
 - chart_4　[棒グラフ] mean_insert_size
 - chart_5　[棒グラフ] duplicate_readsをtotal_readsで割る
 - chart_6　[積み上げグラフ] read_length_r1,read_length_r2

完成したグラフはここ `view <http://genomon-project.github.io/paplot/qc/graph_multi_plot.html>`_ を参照してください。

まず、設定ファイルの [result_format_qc] セクションに入力データの列名を登録します。

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

オプションの列名は次の形式で記述します。 ``col_opt_{name} = {columun name}`` 

``{name}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。

次に、設定ファイルに [qc_chart_1]、[qc_chart_2]、[qc_chart_3] ... セクションを追加し、順番に設定します。

| QCレポートは[qc_chart_1] -> [qc_chart_2] -> [qc_chart_3] の順番に表示し、必要な数だけ [qc_chart_*] セクションを増やすことができます。
| ``*`` には1から始まる連番を入れてください。1から順に表示します。

完成した設定ファイルはここ `config <https://github.com/Genomon-Project/paplot/blob/master/example/qc_multi_plot/paplot.cfg>`_ を参照してください。

3-1. 単純な棒グラフ
---------------------------

chart_1 (average_depth) と chart_4 (mean_insert_size) は単純な棒グラフです。

記載方法は最小構成と同じですので、ここでは割愛します。

3-2. 列同士の数値演算
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

グラフの要素について

| 上記では、 ``stack1 = {mapped_reads/total_reads}`` と記入しています。
| ここで ``{mapped_reads-total_reads}`` と書くと引き算に、 ``{mapped_reads+total_reads}`` と書くと足し算させることができます。
| 
| なお、ポップアップウィンドウでも同様に数値演算させています。
| ``tooltip_format2 = {mapped_reads/total_reads:.2}``
| 
| もし、ポップアップウィンドウではそれぞれの値を表示したい場合は
| ``tooltip_format2 = mapped: {mapped_reads}, total: {total_reads}`` 等と書くとそれぞれの値が表示されます。
|
| ポップアップウィンドウ記述方法詳細は  :ref:`ユーザ定義フォーマット <user_format>` を参照してください。
|

3-3. 積み上げグラフ　その１
-------------------------------------

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

3-4. 積み上げグラフ　その２
-------------------------------------

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

編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_multi_plot/data.csv ./tmp qc_multi_plot \
  --config_file {unzip_path}/example/qc_multi_plot/paplot.cfg

----

.. _qc_brush:

==========================
4. データ選択
==========================

| `view report <http://genomon-project.github.io/paplot/qc/graph_brush.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_brush>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/qc_brush.zip?raw=true>`_ 

前章で作成した複数のグラフに対し、領域選択用のグラフを追加します。

完成したグラフはここ `view <http://genomon-project.github.io/paplot/qc/graph_brush.html>`_ を参照してください。

データ列はaverage_depthを使用します。

もし、新しいデータ列を使用する場合は設定ファイルの [result_format_qc] セクションに col_opt_{name} として登録してください。

領域選択用のグラフは[qc_chart_brush]というセクション名で一つだけ追加することができます。

.. code-block:: cfg
  :caption: example/qc_brush/paplot.cfg
  
  [qc_chart_brush]
  stack = {average_depth}
  name_set = average:#E3E5E9

編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot qc {unzip_path}/example/qc_brush/data.csv ./tmp qc_brush \
  --config_file {unzip_path}/example/qc_brush/paplot.cfg

.. |new| image:: image/tab_001.gif
