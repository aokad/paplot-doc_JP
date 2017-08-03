******************************
Mutational Signature レポート
******************************

ここでは、exampleデータ (※) を基にして、Mutational Signature レポートを出力するために必要な入力データを解説します。

※ exampleデータはpaplotをダウンロードして解凍したディレクトリ中、exampleディレクトリにあります。

:doc:`exec_signature` の手順でデータの準備を行う場合、configファイルの変更は必要ありません。

.. _json:

==========================
1. jsonフォーマット
==========================

paplotで Mutational Signature レポートを作成するためにはこれまでの、 Mutation Matrix や Chromosomal Aberration、QC とは異なり、jsonファイル形式でシグネチャのデータを用意する必要があります。

ここでは、paplotが使用するシグネチャのデータフォーマットについて解説します。

`example/signature_integral/data2.json` ファイルをテキストエディタで開くと次のようになっています。

(長いため一部省略しています)

.. code-block:: python
  :caption: example/signature_integral/data2.json

  {
    "signature":[
                  [ # signature 1
                    [0.0018,0.0003,0.0002,0.0005,0.0014,0.0008,0.0002,0.0007,0.0012,0.0003,0.0002,0.0004,0.0271,0.0107,0.0016,0.0145],  # C > A
                    [0.0023,0.0007,0.0001,0.002,0.0027,0.0005,0.0004,0.0032,0.0007,0.0004,0.0001,0.0013,0.1546,0.0306,0.0055,0.1931],   # C > G
                    [0.0043,0.0016,0.0027,0.0019,0.0096,0.0026,0.0046,0.0053,0.0045,0.0021,0.0034,0.0028,0.2612,0.0517,0.0284,0.1335],  # C > T
                    [0.0012,0.0007,0.0004,0.0003,0.0003,0.0003,0,0,0.0003,0.0001,0.0003,0,0.0005,0.0001,0.0001,0.0002],                 # T > A
                    [0.0008,0.0003,0.0008,0.0007,0.0002,0.0004,0.0009,0.0005,0.0004,0.0003,0.0006,0.0003,0.0003,0.0004,0.0002,0.0004],  # T > C
                    [0.0001,0.0001,0.0001,0.0001,0,0.0001,0.0001,0,0.0001,0.0001,0.0009,0.0002,0.0001,0,0.0001,0.0005]                  # T > G
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

**シグネチャのデータフォーマット**

:signature:
  | シグネチャの各barの値。
  | シグネチャごと、変化パターン (C > A など) ごとに値を記述します。
  | 変化パターンの数を変えることはできません。
  | baseの数は3か5のいずれかのみ設定できます。

今回の例ではbase=3のため次の順に16ケースの値を記述します。(R=Reference) 

::

  ARA,ARC,ARG,ART,CRA,CRA,CRG,CRT,GRA,GRC,GRG,GRT,TRA,TRA,TRG,TRT

もしbase=5とする場合は、次の順に256ケースの記述が必要です。(R=Reference) 

::

  AARAA,AARAC,AARAG,AARAT,AARCA,AARCC,AARCG,AARCT,AARGA,AARGC,AARGG,AARGT,AARTA,AARTC,AARTG,AARTT,
  ACRAA,ACRAC,ACRAG,ACRAT,ACRCA,ACRCC,ACRCG,ACRCT,ACRGA,ACRGC,ACRGG,ACRGT,ACRTA,ACRTC,ACRTG,ACRTT,
  AGRAA,AGRAC,AGRAG,AGRAT,AGRCA,AGRCC,AGRCG,AGRCT,AGRGA,AGRGC,AGRGG,AGRGT,AGRTA,AGRTC,AGRTG,AGRTT,
  ATRAA,ATRAC,ATRAG,ATRAT,ATRCA,ATRCC,ATRCG,ATRCT,ATRGA,ATRGC,ATRGG,ATRGT,ATRTA,ATRTC,ATRTG,ATRTT,
  CARAA,CARAC,CARAG,CARAT,CARCA,CARCC,CARCG,CARCT,CARGA,CARGC,CARGG,CARGT,CARTA,CARTC,CARTG,CARTT,
  CCRAA,CCRAC,CCRAG,CCRAT,CCRCA,CCRCC,CCRCG,CCRCT,CCRGA,CCRGC,CCRGG,CCRGT,CCRTA,CCRTC,CCRTG,CCRTT,
  CGRAA,CGRAC,CGRAG,CGRAT,CGRCA,CGRCC,CGRCG,CGRCT,CGRGA,CGRGC,CGRGG,CGRGT,CGRTA,CGRTC,CGRTG,CGRTT,
  CTRAA,CTRAC,CTRAG,CTRAT,CTRCA,CTRCC,CTRCG,CTRCT,CTRGA,CTRGC,CTRGG,CTRGT,CTRTA,CTRTC,CTRTG,CTRTT,
  GARAA,GARAC,GARAG,GARAT,GARCA,GARCC,GARCG,GARCT,GARGA,GARGC,GARGG,GARGT,GARTA,GARTC,GARTG,GARTT,
  GCRAA,GCRAC,GCRAG,GCRAT,GCRCA,GCRCC,GCRCG,GCRCT,GCRGA,GCRGC,GCRGG,GCRGT,GCRTA,GCRTC,GCRTG,GCRTT,
  GGRAA,GGRAC,GGRAG,GGRAT,GGRCA,GGRCC,GGRCG,GGRCT,GGRGA,GGRGC,GGRGG,GGRGT,GGRTA,GGRTC,GGRTG,GGRTT,
  GTRAA,GTRAC,GTRAG,GTRAT,GTRCA,GTRCC,GTRCG,GTRCT,GTRGA,GTRGC,GTRGG,GTRGT,GTRTA,GTRTC,GTRTG,GTRTT,
  TARAA,TARAC,TARAG,TARAT,TARCA,TARCC,TARCG,TARCT,TARGA,TARGC,TARGG,TARGT,TARTA,TARTC,TARTG,TARTT,
  TCRAA,TCRAC,TCRAG,TCRAT,TCRCA,TCRCC,TCRCG,TCRCT,TCRGA,TCRGC,TCRGG,TCRGT,TCRTA,TCRTC,TCRTG,TCRTT,
  TGRAA,TGRAC,TGRAG,TGRAT,TGRCA,TGRCC,TGRCG,TGRCT,TGRGA,TGRGC,TGRGG,TGRGT,TGRTA,TGRTC,TGRTG,TGRTT,
  TTRAA,TTRAC,TTRAG,TTRAT,TTRCA,TTRCC,TTRCG,TTRCT,TTRGA,TTRGC,TTRGG,TTRGT,TTRTA,TTRTC,TTRTG,TTRTT

**積み上げグラフ描画データ**

この項目はオプションです。

設定するとサンプル毎にシグネチャの積算グラフ ( `例 <http://genomon-project.github.io/paplot/signature/graph_integral2.html>`_ ) を作成します。

:id:
  | サンプル名リスト

:mutation_count:
  | サンプルごとの変異数
  | 上記の例の場合、PD3851a の変異数=4001、PD3890a の変異数=7174、PD3904a の変異数=5804 となります。

:mutation:
  | サンプルごと、シグネチャごとの割合を設定します。 
  | [sample index, signature index, value] の順に記載します。
  |
  | サンプルのindexは id で記載した順に0からカウントします。
  | 上記の例の場合、PD3851a=0、PD3890a=1、PD3904a=2となります。
  |
  | シグネチャのindexも `signature` で記載した順に0からカウントします。
  | 上記の例の場合、signature1 = 0、signature2 = 1、signature3 = 2 となります。

.. note::

  key名は変更可能です。key名を変更した場合は設定ファイル ([result_format_signature] key_*)を変更してください。

  .. code-block:: cfg
    :caption:  paplot/example/signature_integral/paplot.cfg
    
    [result_format_signature]
    # jsonファイルのkey名
    key_signature = signature
    key_id = id
    key_mutation = mutation
    key_mutation_count = mutation_count
            
.. note::

  jsonとしての形式の厳密さについては、paplotはpythonのjsonパッケージを使用しているため、次のコマンドで読めればOKです。

  python jsonパッケージを使用したファイル確認例 (ファイル名が "data2.json" の場合)

  .. code-block:: shell
  
    $ python
    >>> import json
    >>> json.load(open("data2.json"))
  
----

.. _sig_minimal:

==========================
2. 最小データセット
==========================

| `view report <http://genomon-project.github.io/paplot/signature/graph_signature_minimal2.html>`_ 
| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/signature_minimal>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/signature_minimal.zip?raw=true>`_ 

入力データ形式は :ref:`こちら <json>` 参照。

:doc:`exec_signature` の手順でデータの準備を行う場合、configファイルの変更は必要ありません。

ここではpaplotコマンドを中心に解説します。

データファイル (シグネチャ数は2)

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

configファイル

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

``paplot`` を実行します。

.. code-block:: bash

  paplot signature signature_minimal/data.json ./tmp signature_minimal \
  --config_file ./signature_minimal/paplot.cfg


上記のコマンドを実行すると以下の場所にレポートが作成されます。

ここで出力されるレポートは、graph_signature2.html と、シグネチャの数がファイル名に反映されています。

シグネチャの数はpaplot実行時に入力ファイル (data.json) から読み取り、自動的に判定します。

::

  ./tmp
    ┗ signature_minimal
        ┗ graph_signature2.html

.. _data_signature_multi:

----

.. _sig_mclass:

===================================
3. 複数タイプのシグネチャ
===================================

| view report

 - `signature 2 <http://genomon-project.github.io/paplot/signature/graph_multi_class2.html>`_ 
 - `signature 3 <http://genomon-project.github.io/paplot/signature/graph_multi_class3.html>`_ 
 - `signature 4 <http://genomon-project.github.io/paplot/signature/graph_multi_class4.html>`_ 
 - `signature 5 <http://genomon-project.github.io/paplot/signature/graph_multi_class5.html>`_ 
 - `signature 6 <http://genomon-project.github.io/paplot/signature/graph_multi_class6.html>`_ 

| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/signature_multi_class>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/signature_multi_class.zip?raw=true>`_ 

入力データ形式は :ref:`こちら <json>` 参照。

:doc:`exec_signature` の手順でデータの準備を行う場合、configファイルの変更は必要ありません。ここではpaplotコマンドを中心に解説します。

データファイルはシグネチャクラスの数だけ用意し、configファイルは形式が同じであれば一つだけ用意します。

今回の場合、以下のファイル構成になります。

::

  example/signature_multi_class/

     # データファイル
    ┣ data2.json  # signature num = 2
    ┣ data3.json  # signature num = 3
    ┣ data4.json  # signature num = 4
    ┣ data5.json  # signature num = 5
    ┣ data6.json  # signature num = 6

     # configファイル
    ┗ paplot.cfg

``paplot`` を実行します。

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

上記のように一つずつ実行してもよいですが、下記のようにまとめて実行することもできます。

.. code-block:: bash

  paplot "signature signature_multi_class/data*.json" ./tmp signature_multi_class \
  --config_file ./signature_multi_class/paplot.cfg

上記のコマンドを実行すると以下の場所にレポートが作成されます。

ここで出力されるレポートは、graph_signature2.html と、シグネチャの数がファイル名に反映されています。

シグネチャの数はpaplot実行時に入力ファイル (data?.json) のデータから読み取り、自動的に判定します。ファイル名称には依存しません。

::

  ./tmp
    ┗ signature_multi_class
        ┣ graph_signature2.html
        ┣ graph_signature3.html
        ┣ graph_signature4.html
        ┣ graph_signature5.html
        ┗ graph_signature6.html

----

.. _sig_integral:

==========================
4. 積算グラフ
==========================

| view report

 - `signature 2 <http://genomon-project.github.io/paplot/signature/graph_integral2.html>`_ 
 - `signature 3 <http://genomon-project.github.io/paplot/signature/graph_integral3.html>`_ 
 - `signature 4 <http://genomon-project.github.io/paplot/signature/graph_integral4.html>`_ 
 - `signature 5 <http://genomon-project.github.io/paplot/signature/graph_integral5.html>`_ 
 - `signature 6 <http://genomon-project.github.io/paplot/signature/graph_integral6.html>`_ 

| `view dataset <https://github.com/Genomon-Project/paplot/blob/master/example/signature_integral>`_ 
| `download dataset <https://github.com/Genomon-Project/paplot/blob/master/example/signature_integral.zip?raw=true>`_ 

レポートに変異の内訳グラフを追加します。 :ref:`こちら <json_full>` で解説に使用しているデータであり、:doc:`exec_signature` によりデータの準備を行う場合に出力されるデータです。

データフォーマットは :ref:`こちら <json>` 参照。

複数データ実行方法は :ref:`こちら <sig_mclass>` 参照。

.. |new| image:: image/tab_001.gif
