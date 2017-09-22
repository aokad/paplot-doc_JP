******************************
Mutational Signature レポート
******************************

ここでは、サンプルデータ [*]_ を使用して、Mutational Signature レポートを出力するために必要な入力データと設定方法を解説します。

.. [*] サンプルデータは paplot をダウンロードして解凍したディレクトリ中、example ディレクトリにあります。

:doc:`exec_signature` に従いデータを準備する場合、設定ファイルの変更は必要ありません。

.. _json_full:

==========================
1. jsonフォーマット
==========================

paplotで Mutational Signature レポートを作成するためには Mutation Matrix レポートや Chromosomal Aberration レポート、QC レポートとは異なり、jsonファイル形式で変異シグネチャのデータを用意する必要があります。

ここでは、paplotが使用する変異シグネチャのデータフォーマットについて解説します。

exampleのデータファイルをテキストエディタで開くと次のようになっています。(長いため一部省略しています)

.. code-block:: python
  :caption: example/signature_stack/data2.json

  {
    "signature":[
                  [ # signature 1
                    [0.0018,0.0003,0.0002,0.0005,0.0014,0.0008,0.0002,0.0007,0.0012,0.0003,0.0002,0.0004,0.0271,0.0107,0.0016,0.0145],  # C -> A
                    [0.0023,0.0007,0.0001,0.002,0.0027,0.0005,0.0004,0.0032,0.0007,0.0004,0.0001,0.0013,0.1546,0.0306,0.0055,0.1931],   # C -> G
                    [0.0043,0.0016,0.0027,0.0019,0.0096,0.0026,0.0046,0.0053,0.0045,0.0021,0.0034,0.0028,0.2612,0.0517,0.0284,0.1335],  # C -> T
                    [0.0012,0.0007,0.0004,0.0003,0.0003,0.0003,0,0,0.0003,0.0001,0.0003,0,0.0005,0.0001,0.0001,0.0002],                 # T -> A
                    [0.0008,0.0003,0.0008,0.0007,0.0002,0.0004,0.0009,0.0005,0.0004,0.0003,0.0006,0.0003,0.0003,0.0004,0.0002,0.0004],  # T -> C
                    [0.0001,0.0001,0.0001,0.0001,0,0.0001,0.0001,0,0.0001,0.0001,0.0009,0.0002,0.0001,0,0.0001,0.0005]                  # T -> G
                  ],
                  [ # signature 2
                    [0.0266,0.0222,0.0026,0.02,0.0205,0.0145,0.0012,0.0155,0.0155,0.0094,0.0009,0.011,0.0224,0.0177,0.0019,0.0307],
                    [0.0127,0.0079,0.0035,0.0145,0.0058,0.0048,0.0015,0.0115,0.0034,0.0032,0,0.0071,0.0047,0.0145,0.0006,0.0246],
                    [0.0232,0.0099,0.042,0.0184,0.014,0.0108,0.0219,0.02,0.0137,0.0102,0.0264,0.0128,0.0048,0.0186,0.0153,0.0165],
                    [0.0096,0.0084,0.0094,0.0175,0.0075,0.0076,0.0046,0.0123,0.0044,0.0035,0.0028,0.008,0.0176,0.0047,0.0031,0.0139],
                    [0.0245,0.0087,0.0144,0.0235,0.0098,0.0096,0.0051,0.0102,0.0105,0.0053,0.0042,0.0108,0.0114,0.0081,0.0038,0.0098],
                    [0.0046,0.0006,0.0036,0.0035,0.0025,0.0009,0.0028,0.0082,0.0023,0.0005,0.004,0.0048,0.0041,0.0012,0.0056,0.0104]
                  ]
                ],
    "id":["PD3851a","PD3890a","PD3904a"],
    "mutation":[[0,0,0.0594],[0,1,0.7677],[0,2,0.1727],[1,0,0.1474],[1,1,0.4064],[1,2,0.4461]],
    "mutation_count":[4001,7174,5804]
  }

**Mutational Signature レポートを作成するためのデータ要素**

:signature:
  | 変異パターンの確率値です。
  | 各変異シグネチャごと、置換パターン ("C > A" 等) ごと、コンテキスト ("TpCpA > TpApA" 等) ごとにそれぞれの値を記入します。
  | base の数は 3 か 5 のどちらかを設定できますが、混在させることはできません。
  | base とは、変異の位置 (N) を基準として、前後の塩基の数を意味します。base が 3 である場合、前後の塩基の数はそれぞれ 1 つです。base が 5 である場合、前後の塩基の数はそれぞれ 2 つです。

サンプルデータの base は 3 であり、コンテキストとして、次の並び順に 16 ケースの値を記述しています。

::

  ANA,ANC,ANG,ANT,CNA,CNA,CNG,CNT,GNA,GNC,GNG,GNT,TNA,TNA,TNG,TNT

もし base を 5 にする場合は、次の順に 256 ケースの記述が必要です。

::

  AANAA,AANAC,AANAG,AANAT,AANCA,AANCC,AANCG,AANCT,AANGA,AANGC,AANGG,AANGT,AANTA,AANTC,AANTG,AANTT,
  ACNAA,ACNAC,ACNAG,ACNAT,ACNCA,ACNCC,ACNCG,ACNCT,ACNGA,ACNGC,ACNGG,ACNGT,ACNTA,ACNTC,ACNTG,ACNTT,
  AGNAA,AGNAC,AGNAG,AGNAT,AGNCA,AGNCC,AGNCG,AGNCT,AGNGA,AGNGC,AGNGG,AGNGT,AGNTA,AGNTC,AGNTG,AGNTT,
  ATNAA,ATNAC,ATNAG,ATNAT,ATNCA,ATNCC,ATNCG,ATNCT,ATNGA,ATNGC,ATNGG,ATNGT,ATNTA,ATNTC,ATNTG,ATNTT,
  CANAA,CANAC,CANAG,CANAT,CANCA,CANCC,CANCG,CANCT,CANGA,CANGC,CANGG,CANGT,CANTA,CANTC,CANTG,CANTT,
  CCNAA,CCNAC,CCNAG,CCNAT,CCNCA,CCNCC,CCNCG,CCNCT,CCNGA,CCNGC,CCNGG,CCNGT,CCNTA,CCNTC,CCNTG,CCNTT,
  CGNAA,CGNAC,CGNAG,CGNAT,CGNCA,CGNCC,CGNCG,CGNCT,CGNGA,CGNGC,CGNGG,CGNGT,CGNTA,CGNTC,CGNTG,CGNTT,
  CTNAA,CTNAC,CTNAG,CTNAT,CTNCA,CTNCC,CTNCG,CTNCT,CTNGA,CTNGC,CTNGG,CTNGT,CTNTA,CTNTC,CTNTG,CTNTT,
  GANAA,GANAC,GANAG,GANAT,GANCA,GANCC,GANCG,GANCT,GANGA,GANGC,GANGG,GANGT,GANTA,GANTC,GANTG,GANTT,
  GCNAA,GCNAC,GCNAG,GCNAT,GCNCA,GCNCC,GCNCG,GCNCT,GCNGA,GCNGC,GCNGG,GCNGT,GCNTA,GCNTC,GCNTG,GCNTT,
  GGNAA,GGNAC,GGNAG,GGNAT,GGNCA,GGNCC,GGNCG,GGNCT,GGNGA,GGNGC,GGNGG,GGNGT,GGNTA,GGNTC,GGNTG,GGNTT,
  GTNAA,GTNAC,GTNAG,GTNAT,GTNCA,GTNCC,GTNCG,GTNCT,GTNGA,GTNGC,GTNGG,GTNGT,GTNTA,GTNTC,GTNTG,GTNTT,
  TANAA,TANAC,TANAG,TANAT,TANCA,TANCC,TANCG,TANCT,TANGA,TANGC,TANGG,TANGT,TANTA,TANTC,TANTG,TANTT,
  TCNAA,TCNAC,TCNAG,TCNAT,TCNCA,TCNCC,TCNCG,TCNCT,TCNGA,TCNGC,TCNGG,TCNGT,TCNTA,TCNTC,TCNTG,TCNTT,
  TGNAA,TGNAC,TGNAG,TGNAT,TGNCA,TGNCC,TGNCG,TGNCT,TGNGA,TGNGC,TGNGG,TGNGT,TGNTA,TGNTC,TGNTG,TGNTT,
  TTNAA,TTNAC,TTNAG,TTNAT,TTNCA,TTNCC,TTNCG,TTNCT,TTNGA,TTNGC,TTNGG,TTNGT,TTNTA,TTNTC,TTNTG,TTNTT

**寄与度グラフ描画データ**

この項目はオプションです。

寄与度グラフは、各変異シグネチャに関連づけられている変異はどれくらいの数かを示す積み上げグラフです。
入力 json ファイルに **id**, **mutation**, **mutation_count** が設定されている場合、サンプル毎に変異シグネチャの寄与度グラフ ( `例 <http://genomon-project.github.io/paplot/signature_stack/graph_stack2.html>`__ ) を作成します。

:id:
  | サンプル名のリストです。

:mutation_count:
  | サンプルごとの変異数です。
  | 上記の例の場合、PD3851a の変異数=4001、PD3890a の変異数=7174、PD3904a の変異数=5804 となります。

:mutation:
  | サンプルごと、変異シグネチャごとの割合を設定します。 
  | [sample index, signature index, value] の順に記載します。
  |
  | ``sample index`` は ``id`` で記載した順に 0 からカウントします。
  | 上記の例の場合の ``sample index`` は PD3851a=0、PD3890a=1、PD3904a=2 となります。
  |
  | ``signature index`` は ``signature`` で記載した順に 0 からカウントします。
  | 上記の例の場合の ``signature index`` は signature1 = 0、signature2 = 1、background = 2 となります。

.. note::

  キーは変更可能です。キーを変更した場合は設定ファイル (``[result_format_signature]`` セクションの ``key_*`` オプション) を変更してください。

  .. code-block:: cfg
    :caption:  example/signature_stack/paplot.cfg
    
    [result_format_signature]
    # json ファイルのキー
    key_signature = signature
    key_id = id
    key_mutation = mutation
    key_mutation_count = mutation_count
            
.. note::

  json ファイルの確認
  
  paplot は python の json パッケージを使用しているため、次のコマンドで読めれば OK です。

  json パッケージを使用したファイル確認例 (ファイル名が "data2.json" の場合)

  .. code-block:: shell
  
    $ python
    >>> import json
    >>> json.load(open("data2.json"))
  
----

.. _sig_minimal:

==========================
2. 最小データセット
==========================

| `このセクションで生成するレポートを見る <http://genomon-project.github.io/paplot/signature_minimal/graph_signature_minimal2.html>`__ 
| `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/signature_minimal>`__ 
| `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/signature_minimal.zip?raw=true>`__ 

入力データ形式は :ref:`1. jsonフォーマット <json_full>` 参照。

:doc:`exec_signature` の手順でデータの準備を行う場合、設定ファイルの変更は必要ありません。

データファイル (変異シグネチャ数は 2)

.. code-block:: python
  :caption: example/signature_minimal/data.json
  
  {
    "signature":[
      # signature 1
      [ 
        [0.0021,0.0006,0.0002,0.0007,0.0017,0.001,0.0003,0.0009,0.0014,0.0006,0.0003,0.0006,0.027,0.0108,0.0016,0.0147],
        [0.0025,0.0009,0.0002,0.0022,0.0029,0.0007,0.0005,0.0034,0.0009,0.0006,0.0002,0.0014,0.1504,0.0301,0.0053,0.1884],
        [0.0046,0.0018,0.0031,0.0021,0.0097,0.0029,0.0049,0.0055,0.0047,0.0024,0.0037,0.003,0.2557,0.0513,0.0286,0.1312],
        [0.0014,0.0009,0.0007,0.0006,0.0004,0.0005,0.0003,0.0003,0.0004,0.0003,0.0005,0.0002,0.0008,0.0003,0.0003,0.0005],
        [0.001,0.0004,0.0011,0.001,0.0003,0.0007,0.0012,0.0008,0.0006,0.0004,0.0007,0.0005,0.0005,0.0007,0.0004,0.0007],
        [0.0003,0.0003,0.0003,0.0003,0.0001,0.0003,0.0003,0.0003,0.0002,0.0002,0.0011,0.0004,0.0003,0.0002,0.0003,0.0009]
      ],
      # signature 2
      [ 
        [0.022,0.0183,0.0028,0.0171,0.0192,0.0148,0.0026,0.0157,0.0143,0.0108,0.0018,0.0116,0.0181,0.016,0.0021,0.0246],
        [0.0133,0.0088,0.0037,0.0136,0.0095,0.008,0.003,0.0131,0.0065,0.0063,0.0016,0.0095,0.0044,0.0135,0.0016,0.0171],
        [0.0195,0.0098,0.0283,0.0159,0.0138,0.0112,0.0156,0.0183,0.0128,0.0108,0.0186,0.0127,0,0.0146,0.0095,0.0115],
        [0.0095,0.0085,0.0102,0.0155,0.0077,0.0102,0.0096,0.0135,0.0054,0.0052,0.0058,0.0089,0.0145,0.0076,0.0058,0.016],
        [0.0192,0.0089,0.0135,0.0198,0.0089,0.0113,0.0092,0.0117,0.0092,0.0063,0.0064,0.01,0.0107,0.0096,0.0061,0.0123],
        [0.0059,0.0028,0.0068,0.0063,0.0039,0.0044,0.0076,0.0101,0.004,0.0028,0.007,0.0064,0.006,0.0046,0.008,0.0132]
      ]
    ]
  }

設定ファイル

.. code-block:: cfg
  :caption: example/signature_minimal/paplot.cfg
  
  [signature]
  tooltip_format_signature_title = {sig}
  tooltip_format_signature_partial = {route}: {#sum_item_value:6.2}
  
  signature_y_max = -1
  
  alt_color_CtoA = #1BBDEB
  alt_color_CtoG = #211D1E
  alt_color_CtoT = #E62623
  alt_color_TtoA = #CFCFCF
  alt_color_TtoC = #ACD577
  alt_color_TtoG = #EDC7C4
  
  [result_format_signature]
  format = json
  background = False
  key_signature = signature

paplot を実行します。

.. code-block:: bash

  paplot signature signature_minimal/data.json ./tmp signature_minimal \
  --config_file ./signature_minimal/paplot.cfg


上記のコマンドを実行すると以下の場所にレポートが作成されます。

ここで出力されるレポートファイルの名称 ``graph_signature2.html`` には変異シグネチャ数が反映されています。

変異シグネチャ数は paplot 実行時に入力データ (data.json) から paplot が読み取ります。

::

  ./tmp
    ┗ signature_minimal
        ┗ graph_signature2.html

.. _data_signature_multi:

----

.. _sig_mclass:

==========================================
3. 複数データファイルの変異シグネチャ
==========================================

| このセクションで生成するレポートを見る

 - `signature 2 <http://genomon-project.github.io/paplot/signature_multi_class/graph_multi_class2.html>`__ 
 - `signature 3 <http://genomon-project.github.io/paplot/signature_multi_class/graph_multi_class3.html>`__ 
 - `signature 4 <http://genomon-project.github.io/paplot/signature_multi_class/graph_multi_class4.html>`__ 
 - `signature 5 <http://genomon-project.github.io/paplot/signature_multi_class/graph_multi_class5.html>`__ 
 - `signature 6 <http://genomon-project.github.io/paplot/signature_multi_class/graph_multi_class6.html>`__ 

| `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/signature_multi_class>`__ 
| `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/signature_multi_class.zip?raw=true>`__ 

入力データ形式は :ref:`1. jsonフォーマット <json_full>` 参照。

:doc:`exec_signature` の手順でデータの準備を行う場合、設定ファイルの変更は必要ありません。

変異シグネチャ解析においては、クラスタリング数を 2 や 3 などに固定せず、2 ～ 6 など幅を持たせた数で試験的に解析を行い、結果をみて適切なクラスタ数を決定することがあります。

今回のセクションでは、変異シグネチャのデータファイルを複数使用します。

今回の場合、以下のファイル構成になります。

::

  example/signature_multi_class/

     # データファイル
    ┣ data2.json  # signature num = 2
    ┣ data3.json  # signature num = 3
    ┣ data4.json  # signature num = 4
    ┣ data5.json  # signature num = 5
    ┣ data6.json  # signature num = 6

     # 設定ファイル
    ┗ paplot.cfg

変異シグネチャのデータファイルごとに paplot を実行します。

.. code-block:: bash

  paplot signature signature_multi_class/data2.json ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

  paplot signature signature_multi_class/data3.json ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

  paplot signature signature_multi_class/data4.json ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

  paplot signature signature_multi_class/data5.json ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

  paplot signature signature_multi_class/data6.json ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

下記のようにまとめて実行することもできます。

.. code-block:: bash

  paplot signature "signature_multi_class/data*.json" ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

上記のコマンドを実行すると以下の場所にレポートが作成されます。

ここで出力されるレポートファイルの名称 ``graph_signature2.html`` には変異シグネチャ数が反映されています。

変異シグネチャ数は paplot 実行時に入力データ (data.json) から paplot が読み取ります。

::

  ./tmp
    ┗ signature_multi_class
        ┣ graph_signature2.html
        ┣ graph_signature3.html
        ┣ graph_signature4.html
        ┣ graph_signature5.html
        ┗ graph_signature6.html

----

.. _sig_stack:

==========================
4. 寄与度グラフ
==========================

| このセクションで生成するレポートを見る

 - `signature 2 <http://genomon-project.github.io/paplot/signature_stack/graph_stack2.html>`__ 
 - `signature 3 <http://genomon-project.github.io/paplot/signature_stack/graph_stack3.html>`__ 
 - `signature 4 <http://genomon-project.github.io/paplot/signature_stack/graph_stack4.html>`__ 
 - `signature 5 <http://genomon-project.github.io/paplot/signature_stack/graph_stack5.html>`__ 
 - `signature 6 <http://genomon-project.github.io/paplot/signature_stack/graph_stack6.html>`__ 

| `このセクションで使用するデータセットを見る <https://github.com/Genomon-Project/paplot/blob/master/example/signature_stack>`__ 
| `このセクションで使用するデータセットをダウンロードする <https://github.com/Genomon-Project/paplot/blob/master/example/signature_stack.zip?raw=true>`__ 

レポートに変異の内訳グラフを追加します。 :doc:`exec_signature` によりデータの準備を行う場合、あらかじめ出力するように設定しています。

入力データ形式は :ref:`1. jsonフォーマット <json_full>` 参照。

複数データ実行方法は :ref:`3. 複数タイプの変異シグネチャ <sig_mclass>` 参照。

paplot を実行します。

.. code-block:: bash
  
  paplot signature "signature_stack/data*.json" ./tmp signature_stack \
  --config_file ./signature_stack/paplot.cfg

.. |new| image:: image/tab_001.gif
