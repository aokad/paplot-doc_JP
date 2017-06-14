**************************
exampleデータセット
**************************

paplot実行例として以下のデータセットを用意しています。

各項目の記載は最小構成からの差分です。必要に応じてご使用ください。

.. _conf_mm:

1. mutation-matrix
----------------------

 - :download:`download <example/mutation_minimal.zip>`  最小構成
 - :download:`download <example/mutation_option.zip>`   オプション情報追加
 - :download:`download <example/mutation_noheader.zip>` ヘッダなし
 - :download:`download <example/mutation_subplot.zip>`  オプション情報追加、サブプロット付き (※1)
 
※1 paplotのexampleに付属のデータ

.. _conf_qc:

2. QC
------------

 - :download:`download <example/qc_minimal.zip>`    最小構成 (depth average のみ)
 - :download:`download <example/qc_multi_plot.zip>` グラフ情報追加 (※2)
 - :download:`download <example/qc_brush.zip>`      グラフ情報追加、選択グラフ追加 (※3)
 - :download:`download <example/qc_noheader.zip>`   ヘッダなし

※2 以下のグラフを表示しています。
 
 - depth coverage (30x, 20x, 10x, 2x の積み上げグラフ)
 - depth average
 - マップリード率 (mapped_reads/total_reads)
 - mean_insert_size
 - 重複リード率 (duplicate_reads/total_reads)
 - リード長 (read_length_r1,read_length_r2 の積み上げグラフ)

※3 paplotのexampleに付属のデータです。※2に対し、レポート先頭に選択用のグラフを追加しています。

.. _conf_ca:

3. CA
--------------

 - :download:`download <example/ca_minimal.zip>`  最小構成
 - :download:`download <example/ca_option.zip>`   オプション情報追加 (※)
 - :download:`download <example/ca_noheader.zip>` ヘッダなし

※ paplotのexampleに付属のデータ

.. _conf_signature:

4. signature
---------------------------

 - :download:`download <example/signature_minimal.zip>`     最小構成 (クラスタリング数 = 3)
 - :download:`download <example/signature_multi_class.zip>` 複数クラス (クラスタリング数 = 3～6)（※）

※ paplotのexampleに付属のデータ

.. _conf_pmsignature:

5. pmsignature
---------------------------

 - :download:`download <example/pmsignature_minimal.zip>`      最小構成 (クラスタリング数 = 3)
 - :download:`download <example/pmsignature_multi_class.zip>`  複数クラス (クラスタリング数 = 3～6)（※）
 - :download:`download <example/pmsignature_nobackground.zip>` backgroundなし

※ paplotのexampleに付属のデータ

.. |new| image:: image/tab_001.gif
