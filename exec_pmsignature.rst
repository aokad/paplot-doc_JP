**********************************************
pmsignature 実行手順
**********************************************

ここでは `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を使用した場合のデータの準備方法を解説します。

.. note::

  | 実行前に R の環境構築と pmsignature および関連パッケージのインストールが必要です。
  | インストールおよび、実行コマンドの詳しい解説は `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を参照ください。
  |
  | 別のツールを用いて pmsignature 解析を行った場合は、 `仕様 <./data_pmsignature.html#json-ind>`_ に準拠する json ファイルを別途準備ください。
  
1. 結果ファイルの整形
-----------------------------

`signature <./exec_signature.html#pre>`_ 参照
 
2. pmsignature の実行
-----------------------------

pmsignature を ``type="independent"`` (default) で実行したのち、パラメータを `.Rdata` ファイルに出力します。

今回の例では、pmsignatureのサンプルデータを使用しているため .txt.gz 形式ですが、1の結果ファイルを入力する場合は圧縮する必要はありません。

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

3. paplot で使用できるように Rdata を変換する
-----------------------------------------------------

4で作成した"pmsignature_ind3.Rdata" ファイルをpaplotで読み込めるように .json 形式に変換します。

変換スクリプトを用意していますので、以下より最新版をダウンロードし、適切な場所に解凍してください。
インストールの必要はありません。

https://github.com/Genomon-Project/genomon_Rscripts/releases

入力ファイル、出力したいファイル名の順に引数を渡します。

.. code-block:: bash

  R --vanilla --slave --args ./pmsignature_ind3.Rdata ./pmsignature_ind3.json \
  < {path to genomon_Rscripts}/pmsignature/convert_toJson_ind.R


4. paplotの実行
-----------------------------

2で作成した "pmsignature_ind3.json" ファイルを使用して、paplot を実行します。上述の方法で実行した場合、設定ファイルの変更は必要ありません。

paplot 実行例

.. code-block:: bash

  paplot signature pmsignature_ind3.Rdata ./temp signature_test

.. |new| image:: image/tab_001.gif
