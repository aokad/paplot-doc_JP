**********************************************
実行手順 (signature) |new|
**********************************************

ここでは `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を使用した場合のデータの準備方法を解説します。

.. note::

  | 実行前にRの環境構築とpmsignatureおよび関連パッケージのインストールが必要です。
  | インストールおよび、実行コマンドの詳しい解説は `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を参照ください。
  |
  | 別のツールを用いてsignature解析を行った場合は、:ref:`仕様 <json_full>` に準拠するjsonファイルを別途準備ください。

1. pmsignatureの実行
-----------------------------

pmsignatureを ``type="full"`` で実行してパラメータを出力します。

今回の例では、pmsignatureのサンプルデータを使用しています。

.. code-block:: R

  library(pmsignature)
  
  # use sample data
  inputFile <- system.file("extdata/Nik_Zainal_2012.mutationPositionFormat.txt.gz", package="pmsignature")
  G <- readMPFile(inputFile, numBases = 3, type = "full", trDir = FALSE)
  
  # use background
  BG_prob <- readBGFile(G)
  
  Param <- getPMSignature(G, K = 3, BG = BG_prob)
  Boot <- bootPMSignature(G, Param0 = Param, bootNum = 100, BG = BG_prob)
  
  # save .Rdata
  resultForSave <- list(Param, Boot)
  save(resultForSave, file="pmsignature_full3.Rdata")

2. paplotで使用できるように結果ファイルを変換する
-----------------------------------------------------

1で作成した"pmsignature_full3.Rdata" ファイルをpaplotで読み込めるように.json形式に変換します。

変換スクリプトを用意していますので、以下より最新版をダウンロードし、適切な場所に解凍してください。
インストールの必要はありません。

https://github.com/Genomon-Project/genomon_Rscripts/releases

入力ファイル, 出力したいファイル名の順に引数を渡します。

.. code-block:: bash

  R --vanilla --slave --args ./pmsignature_full3.Rdata ./pmsignature_full3.json < {path to genomon_Rscripts}/pmsignature/convert_toJson_full.R


3. paplotの実行
-----------------------------

2で作成した"pmsignature_full3.json" ファイルを使用して、paplot を実行します。上述の方法で実行した場合、configファイルの変更は必要ありません。

.. note::

  backgroundを使用しない場合は、configファイルのbackgroundをFalseに変更してください。

`paplot signature pmsignature_full3.Rdata ./temp signature_test`


.. _json_full:

[補足] jsonフォーマット
-----------------------------


| `example/signature/Nik_Zainal_2012.full.3.json` ファイルをテキストエディタで開くと次のようになっています。
| (長いため一部省略しています)
|

.. code-block:: python

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

**signature描画データ**

:signature:
  | signatureの各barの値。
  | signatureごと、変化パターン (C > A など) ごとに値を記述します。
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

:id:
  | サンプル名リスト

:mutation_count:
  | サンプルごとのmutation数
  | 上記の例の場合、PD3851a のmutation数=4001, PD3890a のmutation数=7174, PD3904a のmutation数=5804 となります。

:mutation:
  | サンプルごと、signatureごとの割合を設定します。 
  | [sample index, signature index, value] の順に記載します。
  |
  | サンプルのindexは id で記載した順に0からカウントします。
  | 上記の例の場合、PD3851a=0, PD3890a=1, PD3904a=2となります。
  |
  | signatureのindexも ref で記載した順に0からカウントします。
  | backgroundを使用する場合、signature1, signature2, ..., backgroundの順にカウントします。
  | 上記の例の場合、signature1 = 0, signature2 = 1, background = 2となります。

.. note::

  key名は変更可能です。key名を変更した場合は設定ファイル ([result_format_signature] key_*)を変更してください。

.. note::

  jsonとしての形式の厳密さについては、paplotはpythonのjsonパッケージを使用しているため、次のコマンドで読めればOKです。

  python jsonパッケージを使用したファイル確認例 (ファイル名が "Nik_Zainal_2012.full.3.json" の場合)

  .. code-block:: shell
  
    $ python
    >>> import json
    >>> json.load(open("Nik_Zainal_2012.full.3.json"))
  

.. |new| image:: image/tab_001.gif
