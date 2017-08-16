**************************
Mutation Matrix レポート
**************************

ここでは、サンプルデータ (※) を使用して、Mutation Matrix レポートを出力するために必要な入力データと設定方法を解説します。

※ サンプルデータは paplot をダウンロードして解凍したディレクトリ中、example ディレクトリにあります。

.. _mm_minimal:

==========================
1. 最小データセット
==========================

 * `このセクションで生成するレポートを見る <http://genomon-project.github.io/paplot/mutation_minimal/graph_minimal.html>`_ 
 * `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_minimal>`_ 
 * `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_minimal.zip?raw=true>`_ 

paplot で Mutation Matrix を作成するために最低限必要な項目はサンプルID (Sample)、遺伝子名 (Gene)、変異タイプ (MutationType) の3つです。

.. code-block:: cfg
  :caption: データファイルから一部抜粋 (example/mutation_minimal/data.csv)
  
  Sample,MutationType,Gene
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

今回の例では列名は Sample, MutationType, Gene としていますが、任意に設定できます。

設定ファイルの [result_format_mutation] セクションでデータの列名を次のように設定します。

.. code-block:: cfg
  :caption: example/mutation_minimal/paplot.cfg

  [result_format_mutation]
  # column index (required)
  col_group = MutationType
  col_gene = Gene
  
  # column index (option)
  col_opt_id = Sample


編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_minimal/data.csv ./tmp mutation_minimal \
  --config_file {unzip_path}/example/mutation_minimal/paplot.cfg

----

.. _mm_noheader:

==========================
2. ヘッダなし
==========================

| `このセクションで生成するレポートを見る <http://genomon-project.github.io/paplot/mutation_noheader/graph_noheader.html>`_ 
| `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_noheader>`_ 
| `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_noheader.zip?raw=true>`_ 

.. code-block:: cfg
  :caption: データファイルから一部抜粋 (example/mutation_noheader/data.csv)

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
列番号は左から順に 1 始まりで数えます。

設定ファイルの [result_format_mutation] セクションでデータの列番号を次のように設定します。

.. code-block:: cfg
  :caption: example/mutation_noheader/paplot.cfg
  
  [result_format_mutation]
  # ヘッダオプションを False に設定する
  header = False
  
  # column index (required)
  col_group = 2
  col_gene = 3
  
  # column index (option)
  col_opt_id = 1

編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_noheader/data.csv ./tmp mutation_noheader \
  --config_file {unzip_path}/example/mutation_noheader/paplot.cfg

----

.. _mm_option:

===================================
3. ポップアップの情報追加
===================================

| `このセクションで生成するレポートを見る <http://genomon-project.github.io/paplot/mutation_option/graph_option.html>`_ 
| `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_option>`_ 
| `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_option.zip?raw=true>`_ 

マウスカーソルを乗せた時に表示する情報 (ポップアップ) をカスタマイズすることができます。

最小構成で表示するポップアップ（グリッド部分）はこのようになっています。

**変更前**

.. image:: image/data_mut1.png

情報を追加して変異の場所や内容を確認できるようにします。

**変更後**

.. image:: image/data_mut2.png

.. code-block:: cfg
  :caption: データファイルから一部抜粋 (example/mutation_option/data.csv)
  
  Sample,Chr,Start,End,Ref,Alt,MutationType,Gene
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

今回の例では、必須項目であるサンプルID (Sample)、遺伝子名 (Gene)、変異タイプ (MutationType) に加えて、
染色体 (Chr)、変異開始位置 (Start)、変異終了位置 (End)、リファレンスの塩基 (Ref)、変異の塩基 (Alt) を追加しています。

まず、追加した列名を設定ファイルに記載します。

設定ファイルの [result_format_mutation] セクションでデータの列名を次のように設定します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [result_format_mutation]
  # column index (option)
  col_opt_chr = Chr
  col_opt_start = Start
  col_opt_end = End
  col_opt_ref = Ref
  col_opt_alt = Alt

オプションの列名は次の形式で記述します。 ``col_opt_{キーワード} = {実際の列名}`` 

 - ``{キーワード}`` の部分は任意に設定できますが、 ``col_opt_`` を必ず先頭につけてください。
 - ``{キーワード}`` には半角英数字 (1-9, a-z, A-Z) および "_" 以外は使用できません。
 - ``col_opt_id`` は予約済みですので、サンプルID以外の用途には使用できません。
 
次に、ポップアップの表示内容を変更します。

.. code-block:: cfg
  :caption: example/mutation_option/paplot.cfg
  
  [mutation]
  # 最小構成での設定
  # tooltip_format_checker_partial = Mutation Type[{group}]
  # 次のように変更
  tooltip_format_checker_partial = Mutation Type[{group}], {chr}:{start}:{end}, [{ref} -> {alt}]

編集した設定ファイルを使用して ``paplot`` を実行します。

.. code-block:: bash

  paplot mutation {unzip_path}/example/mutation_option/data.csv ./tmp mutation_option \
  --config_file {unzip_path}/example/mutation_option/paplot.cfg

今回はグリッド部分のポップアップを変更しました。その他のポップアップ設定項目は `ポップアップの表示内容 <./config.html#mm-tooltip>`_ を参照してください。

また、記載方法に関するより詳細な解説は `ユーザ定義フォーマット <./data_common.html#user-format>`_ を参照してください。

.. |new| image:: image/tab_001.gif
