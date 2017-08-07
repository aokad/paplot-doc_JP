**********************************************
Mutaitonal Signature 実行手順
**********************************************

ここでは `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を使用した場合のデータの準備方法を解説します。

.. note::

  | 実行前にRの環境構築とpmsignatureおよび関連パッケージのインストールが必要です。
  | インストールおよび、実行コマンドの詳しい解説は `pmsignature <https://github.com/friend1ws/pmsignature/>`_ を参照ください。
  |
  | 別のツールを用いてシグネチャ解析を行った場合は、 `仕様 <./data_signature.html#json>`_ に準拠するjsonファイルを別途準備ください。

.. _pre:

1. 結果ファイルの整形
-----------------------------

pmsignatureに入力する変異のデータファイルは以下のフォーマットである必要があります。

 - ヘッダなし、コメント行なし
 - 左から、サンプルID、クロモソーム（chr必要）、posision、リファレンスの塩基、変異の塩基
 - タブ区切り

余分なデータ列は取り除いてください。

::

  PD3851a chr1    809687  G       C
  PD3851a chr1    819245  G       T
  PD3851a chr1    1911011 C       G
  PD3945a chr5    143183408       G       T
  PD3945a chr5    143240819       C       A

テキストの整形には表計算ソフト等を用いるのが最も簡単ですが、データ列の取り出しだけであれば以下のようなコマンドの組み合わせで実行することもできます。

.. code-block:: bash

  input_file={入力ファイル}
  
  # 1,2,3,5,6番目の列を取り出す例
  cut -s -f 1,2,3,5,6 $input_file > ./output.txt
  
  # 順番を入れ替える例 (1番目の列を最後に移動する)
  cut -s -f 1 $input_file > ./tmp1.txt
  cut -s -f 2,3,4,5 $input_file > ./tmp2.txt
  paste ./tmp2.txt ./tmp1.txt > ./output.txt
  
  # chrを先頭につける例 (2番目の列がchr列とする)
  cut -s -f 2 $input_file | sed "s/^/chr/" | sed -e "s/^chr[Cc]hr/chr/g" > tmp1.txt
  
  # 先頭1行がヘッダなので取り除く例
  tail -n +2 $input_file > tmp1.txt

2. pmsignatureの実行
-----------------------------

pmsignatureを ``type="full"`` で実行してパラメータを出力します。

今回の例では、pmsignatureのサンプルデータを使用しているため .txt.gz 形式ですが、1の結果ファイルを入力する場合は圧縮する必要はありません。

.. code-block:: R
  :caption: R console

  library(pmsignature)
  
  # use sample data
  inputFile <- system.file("extdata/Nik_Zainal_2012.mutationPositionFormat.txt.gz", package="pmsignature")
  G <- readMPFile(inputFile, numBases = 3, type = "full", trDir = FALSE)
  
  Param <- getPMSignature(G, K = 3)
  Boot <- bootPMSignature(G, Param0 = Param, bootNum = 100)
  
  # save .Rdata
  resultForSave <- list(Param, Boot)
  save(resultForSave, file="pmsignature_full3.Rdata")

3. paplotで使用できるようにRdataを変換する
-----------------------------------------------------

2で作成した"pmsignature_full3.Rdata" ファイルをpaplotで読み込めるように.json形式に変換します。

変換スクリプトを用意していますので、以下より最新版をダウンロードし、適切な場所に解凍してください。
インストールの必要はありません。

https://github.com/Genomon-Project/genomon_Rscripts/releases

入力ファイル、出力したいファイル名の順に引数を渡します。

.. code-block:: bash

  R --vanilla --slave --args ./pmsignature_full3.Rdata ./pmsignature_full3.json \
  < {path to genomon_Rscripts}/pmsignature/convert_toJson_full.R


※ Rパッケージ "rjson" が必要です。ロードエラーが発生した場合はインストールしてください。

3. paplotの実行
-----------------------------

2で作成した"pmsignature_full3.json" ファイルを使用して、paplot を実行します。上述の方法で実行した場合、設定ファイルの変更は必要ありません。

paplot実行例

.. code-block:: bash

  paplot signature pmsignature_full3.Rdata ./temp signature_test

.. |new| image:: image/tab_001.gif
