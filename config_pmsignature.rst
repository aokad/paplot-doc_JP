**********************************************
実行手順 (pmsignature) |new|
**********************************************

ここでは `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を使用した場合のデータの準備方法を解説します。

.. note::

  | 実行前にRの環境構築とpmsignatureおよび関連パッケージのインストールが必要です。
  | インストールおよび、実行コマンドの詳しい解説は `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を参照ください。
  |
  | 別のツールを用いてsignature解析を行った場合は、:ref:`仕様 <json_ind>` に準拠するjsonファイルを別途準備ください。

1. pmsignatureの実行
-----------------------------

pmsignatureを ``type="independent"`` (default) で実行したのち、パラメータを `.Rdata` ファイルに出力します。

今回の例では、pmsignatureのサンプルデータを使用しています。

.. code-block:: R

  library(pmsignature)
  
  # use sample data
  inputFile <- system.file("extdata/Nik_Zainal_2012.mutationPositionFormat.txt.gz", package="pmsignature")
  G <- readMPFile(inputFile, numBases = 5, trDir = TRUE)
  
  # use background
  BG_prob <- readBGFile(G)
  
  Param <- getPMSignature(G, K = 3, BG = BG_prob)
  Boot <- bootPMSignature(G, Param0 = Param, bootNum = 100, BG = BG_prob)
  
  # save .Rdata
  resultForSave <- list(Param, Boot)
  save(resultForSave, file="pmsignature_ind3.Rdata")

2. paplotで使用できるように結果ファイルを変換する
-----------------------------------------------------

1で作成した"pmsignature_ind3.Rdata" ファイルをpaplotで読み込めるように.json形式に変換します。

変換スクリプトを用意していますので、以下より最新版をダウンロードし、適切な場所に解凍してください。
インストールの必要はありません。

https://github.com/Genomon-Project/genomon_Rscripts/releases


入力ファイル, 出力したいファイル名の順に引数を渡します。

.. code-block:: bash

  R --vanilla --slave --args ./pmsignature_ind3.Rdata ./pmsignature_ind3.json < {path to genomon_Rscripts}/pmsignature/convert_toJson_ind.R

ここで作成した "pmsignature_ind3.json" ファイルをpaplotに入力します。

3. paplotの実行
-----------------------------

2で作成した"pmsignature_ind3.json" ファイルを使用して、paplot を実行します。上述の方法で実行した場合、configファイルの変更は必要ありません。

.. note::

  backgroundを使用しない場合は、configファイルのbackgroundをFalseに変更してください。

`paplot signature pmsignature_ind3.Rdata ./temp signature_test`


.. _json_ind:

[補足] jsonフォーマット
-----------------------------

| `example/pmsignature/Nik_Zainal_2012.ind.3.json` ファイルをテキストエディタで開くと次のようになっています。
| (長いため一部省略しています)
|

.. code-block:: python

  {
    "ref":[
            [ # signature 1
              [0.338,0.15,0.183,0.327],  # ref1 (A,C,G,T)
              [0.362,0.191,0.177,0.267], # ref2 (A,C,G,T)
              [0,0.731,0,0.268],         # ref3 (A,C,G,T)
              [0.31,0.165,0.251,0.272],  # ref4 (A,C,G,T)
              [0.295,0.193,0.168,0.341]  # ref5 (A,C,G,T)
            ],
            [ # signature 2
              [0.179,0.414,0.084,0.321],
              [0.007,0.025,0.004,0.962],
              [0,0.999,0,0],
              [0.472,0.104,0.041,0.381],
              [0.277,0.175,0.284,0.262]
            ]
          ],
    "alt":[
            [ # signature 1
              [0,0,0,0],                 # altA (A,C,G,T)
              [0.194,0,0.091,0.445],     # altC (A,C,G,T)
              [0,0,0,0],                 # altG (A,C,G,T)
              [0.093,0.163,0.011,0]      # altT (A,C,G,T)
            ],
            [ # signature 2
              [0,0,0,0],
              [0.059,0,0.437,0.502],
              [0,0,0,0],
              [0,0,0,0]
            ]
          ],
    "strand":[
              [0.461,0.538],  # signature 1
              [0.512,0.487]   # signature 2
             ],
    "id":["PD3851a","PD3890a","PD3904a"],
    "mutation":[[0,0,0.535],[0,1,0.038],[0,2,0.426],[1,0,0.186],[1,1,0.156],[1,2,0.656]],
    "mutation_count":[702,2312,2096]
  }

.. image:: image/conf_pmsig1.PNG

**signature描画データ**

:ref:
  | signatureの各リファレンスの値。
  | signatureごと、リファレンスごとにA,C,G,Tの順に値を記述します。描画時に再計算しますので、合計して1になる必要はありません。
  | 今回の例ではbaseの数が5ですが、3や7など奇数の数値であれば変更可能です。

:alt:
  | signatureのaltの値。
  | signatureごとに16個の値を設定します。
  | 横方向のサイズはref3 (base=5の場合。base=3であればref2, base=7であればref4) のACGTの各値に従うため、altAとaltGについては通常は0を設定します。

:strand:
  | signatureのstrandの値。
  | signatureごとにplus, minus2つの値をそれぞれ設定します。
  | strandが無い場合は `[0,0]` を記入します。

**積み上げグラフ描画データ**

:id:
  | サンプル名リスト

:mutation_count:
  | サンプルごとのmutation数
  | 上記の例の場合、PD3851a のmutation数=702, PD3890a のmutation数=2312, PD3904a のmutation数=2096 となります。

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

  key名は変更可能です。key名を変更した場合は設定ファイル ([result_format_pmsignature] key_*)を変更してください。

.. note::

  jsonとしての形式の厳密さについては、paplotはpythonのjsonパッケージを使用しているため、次のコマンドで読めればOKです。

  python jsonパッケージを使用したファイル確認例 (ファイル名が "Nik_Zainal_2012.ind.3.json" の場合)

  .. code-block:: shell
  
    $ python
    >>> import json
    >>> json.load(open("Nik_Zainal_2012.ind.3.json"))
  

.. |new| image:: image/tab_001.gif
