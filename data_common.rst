**************************
共通項目
**************************

ここでは、サンプルデータ [*]_ を使用して、それぞれのレポートで共通している事柄について解説します。

.. [*] サンプルデータは paplot をダウンロードして解凍したディレクトリ中、example ディレクトリにあります。

.. _sept:

==========================
1. データ区切り
==========================

データファイルがタブ区切りであった場合、次のように設定します。

.. code-block:: cfg

  # Mutation Matrix レポートの場合
  [result_format_mutation]
  sept = \t

  # スペース区切りの場合
  sept = " "

QC レポートの場合は ``[result_format_qc]`` セクション、Chromosomal Aberration レポートの場合は ``[result_format_ca]`` セクションを変更してください。

----

.. _comment:

==========================
2. コメント行
==========================

.. code-block:: cfg
  
  # This is comment.
  # Please skip this line.
  
  ID,Type,Gene
  SAMPLE00,intronic,GATA3
  SAMPLE00,UTR3,CDH1

このようにデータファイルにコメント行がある場合、次のようにコメント行の開始文字を設定することで、読み飛ばしできます。
開始文字が統一されていない場合は読み飛ばしできませんので、手動で削除してください。

.. code-block:: cfg

  # Mutation Matrix レポートの場合
  [result_format_mutation]
  comment = #

QC レポートの場合は ``[result_format_qc]`` セクション、Chromosomal Aberration レポートの場合は ``[result_format_ca]`` セクションを変更してください。


----

.. _suffix:

======================================
3. データファイルが分かれている場合
======================================

多くの場合、がんゲノム研究においては複数のシーケンスデータを使用します。paplot が生成するレポートも複数のサンプルの情報で構成されています。
paplot で複数のサンプルを使用して入力データを準備するには、次の2つの方法があります。


 - case1: マージされたファイルを入力する
 
   この場合、サンプル名が記述されたデータ列があるはずです。 ``col_opt_id`` で指定してください。

 - case2: サンプルごとに分かれたファイルを入力する
 
   ファイル名の一部をサンプル名として使用します。 ``suffix`` を必ず指定してください。

   
これまでのサンプルでは、case1 について記述してきました。ここでは case2 の入力方法を解説します。

| `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_split_file>`_ 
| `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/mutation_split_file.zip?raw=true>`_ 

今回の例では以下のようにサンプル毎にデータが分かれています。

::

  example/mutation_split_file/

     # データファイル
    ┣ SAMPLE00.data.csv  # SAMPLE00の結果ファイル
    ┣ SAMPLE01.data.csv  # SAMPLE01の結果ファイル
    ┣ SAMPLE02.data.csv  # SAMPLE02の結果ファイル
    ┣ SAMPLE03.data.csv  # SAMPLE03の結果ファイル
    ┣ SAMPLE04.data.csv  # SAMPLE04の結果ファイル

     # 設定ファイル
    ┗ paplot.cfg

.. code-block:: cfg
  :caption: データファイルから一部抜粋 (example/mutation_split_file/SAMPLE00.data.csv)

  MutationType,Gene
  intronic,GATA3
  intronic,FLT3
  intronic,FLT3
  UTR3,CDH1
  exonic,GATA3

設定ファイルで ``suffix`` を設定します。

.. code-block:: cfg
  :caption: example/mutation_split_file/paplot.cfg

   [result_format_mutation]
   suffix = .data.csv
   
   # 今回は col_opt_id は使用しません
   col_opt_id = 

``suffix`` を指定すると、``suffix`` 手前までのファイル名をサンプル名として使用します。

.. image:: image/id_suffix.PNG
  :scale: 100%

編集した設定ファイルを使用して paplot を実行します。

.. code-block:: bash

  # Mutation Matrix レポートの場合
  
  # 複数ファイル指定する場合は , で区切る
  paplot mutation {unzip_path}/example/mutation_split_file/SAMPLE00.data.csv,{unzip_path}/example/mutation_split_file/SAMPLE01.data.csv ./tmp mutation_split_file \
  --config_file {unzip_path}/example/mutation_split_file/paplot.cfg

  # ワイルドカードを使用して、まとめて指定することも可能
  # 最初と最後に " を付けること
  paplot mutation "{unzip_path}/example/mutation_split_file/*.csv" ./tmp mutation_split_file \
  --config_file {unzip_path}/example/mutation_split_file/paplot.cfg

QC レポートの場合は ``[result_format_qc]`` セクション、Chromosomal Aberration レポートの場合は ``[result_format_ca]`` セクションを変更してください。

.. _keyword:

==============================
4. キーワード
==============================

4-1. キーワードとは
----------------------------

paplot では設定ファイルに記入した各データ列をキーワードとして使用できます。

設定ファイルで次のように記入したとします。

.. code-block:: cfg
  
  [result_format_mutation]
  # 必須項目
  # col_{key} = {実際の列名}
  #
  col_gene = Gene
  col_group = MutationType
  
  # オプション
  # col_opt_{key} = {実際の列名}
  #
  col_opt_id = Sample
  col_opt_start = Start
  col_opt_end = End

``col_{key} = {実際の列名}`` もしくは ``col_opt_{key} = {実際の列名}`` と記入した項目のうち、``{key}`` がキーワードになります。

キーワードは任意で増やすことができますが、以下の点にご注意ください。

 - 大文字と小文字の区別はありません。たとえば、CHR、Chr、chr はすべて同一とみなしますので、ご注意ください。
 - 半角英数字 (1-9, a-z, A-Z) および "_" 以外は使用できません。
 - ``col_opt_id`` は予約済みですので、サンプル名以外の用途には使用できません。
 - Mutation Matrix レポートと Chromosomal Aberration レポートにおいては ``col_opt_group`` も予約済みですので、グループ化以外の用途には使用できません。
 - Mutational Signature レポートと pmsignature レポートには追加できません。

.. _user_format:

==============================
5. ユーザ定義フォーマット
==============================

マウスカーソルを乗せた時に表示する情報 (ポップアップ) の内容はある程度変更することができます。

表示箇所ごとにそれぞれ設定しますが、書き方は同一です。

**設定例**

::

  tooltip_format_checker_partial = type[{func}], {chr}:{start}:{end}, [{ref} -> {alt}]
  
  表示例：
  type[exome], chr1:2000:2001, [A -> T]

{} で囲った文字がキーワードで、実際の値に置き換えられます。

`キーワードとは <./data_common.html#keyword>`_ 

5-1. 数値計算
----------------------------

キーワードを 1 つ以上使用して数値計算させることもできます。その場合、計算式を {} で囲います。

::
  
  {key1/key2*100}%
  
  表示例：
  3.33333333333333%

表示桁数を指定したい場合は計算式の後に ``:.2`` と書きます。小数点以下3桁の場合は ``:.3`` と書きます。

::

  {key1/key2*100:.2}%
  
  表示例：
  3.33%

5-2. 桁区切り
----------------------------

数値に桁区切りを付けて表示したい場合、キーワードの後に ``:,`` と書きます。

::
  
  {key1}%
  
  表示例：
  123456789

::

  {key1:,}%
  
  表示例：
  123,456,789


.. |new| image:: image/tab_001.gif
