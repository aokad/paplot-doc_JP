**********************************************
実行準備 (signature, pmsignature) |new|
**********************************************

ここでは `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を使用した場合のデータの準備方法を解説します。

※pmsignatureはRパッケージです。実行前にRの環境構築と関連パッケージのインストールが必要です。
インストールおよび、実行コマンドの詳しい解説は `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を参照ください。

別のツールを用いてsignature解析を行った場合は、仕様に準拠するjsonファイルを別途準備ください。

pmsignature
-----------------------------

pmsignatureを ``type="independent"`` (default) で実行してパラメータを出力します。

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


.Rdataをpaplotで読み込めるように.json形式に変換します。

変換スクリプトを用意していますので、以下より最新版をダウンロードし、適切な場所に解凍してください。
インストールの必要はありません。

https://github.com/Genomon-Project/genomon_Rscripts/releases


↑で出力したファイル, 出力したいファイル名の順に引数を渡します。

.. code-block:: bash

  R --vanilla --slave --args ./pmsignature_ind3.Rdata ./pmsignature_ind3.json < {path to genomon_Rscripts}/pmsignature/convert_toJson_ind.R


signature
-----------------------------

pmsignatureを ``type="full"`` で実行してパラメータを出力します。

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
  resultForSave <- list(Param, Boot);
  save(resultForSave, file="pmsignature_full3.Rdata");


.Rdataをpaplotで読み込めるように.json形式に変換します。

変換スクリプトを用意していますので、以下より最新版をダウンロードし、適切な場所に解凍してください。
インストールの必要はありません。

https://github.com/Genomon-Project/genomon_Rscripts/releases


↑で出力したファイル, 出力したいファイル名の順に引数を渡します。

.. code-block:: bash

  R --vanilla --slave --args ./pmsignature_full3.Rdata ./pmsignature_full3.json < convert_toJson_full.R


実行
-----------------------------

jsonファイルが出力されれば、paplot を実行します。configファイルの変更は必要ありません。


.. |new| image:: image/tab_001.gif
