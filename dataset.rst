**************************
データセット
**************************

paplot実行例として以下のデータセットを用意しています。

各項目に最小構成からの差分を記述しています。必要に応じてご使用ください。

.. _conf_mm:

1. mutation-matrix
----------------------

 * :download:`download <dataset/mutation_minimal.zip>`     最小構成
   + :download:`download <dataset/mutation_option.zip>`    オプション情報追加
     - :download:`download <dataset/mutation_subplot.zip>` オプション情報追加、サブプロット付き (※1)
   + :download:`download <dataset/mutation_noheader.zip>`  ヘッダなし
 
| ※1 paplot付属のexampleと同等の設定

.. _conf_qc:

2. QC
------------

 * :download:`download <dataset/qc_minimal.zip>`      最小構成 (depth average のみ)
   + :download:`download <dataset/qc_multi_plot.zip>` グラフ情報追加 (※2)
     - :download:`download <dataset/qc_brush.zip>`    グラフ情報追加、選択グラフ追加 (※3)
   + :download:`download <dataset/qc_noheader.zip>`   ヘッダなし

| ※2 以下のグラフを追加しています。
|  
|  - depth coverage (30x, 20x, 10x, 2x の積み上げグラフ)
|  - マップリード率 (mapped_reads/total_reads)
|  - mean_insert_size
|  - 重複リード率 (duplicate_reads/total_reads)
|  - リード長 (read_length_r1,read_length_r2 の積み上げグラフ)

| ※3 paplot付属のexampleと同等の設定です。※2に対し、レポート先頭に選択用のグラフを追加しています。

.. _conf_ca:

3. CA
--------------

 * :download:`download <dataset/ca_minimal.zip>`    最小構成
   + :download:`download <dataset/ca_option.zip>`   グループ情報追加
     - :download:`download <dataset/ca_option.zip>` グループ情報追加、オプション情報追加 (※4)
   + :download:`download <dataset/ca_noheader.zip>` ヘッダなし

| ※4 paplot付属のexampleとほぼ同等の設定です（グルーピングの色が違います）

.. _conf_signature:

4. signature
---------------------------

 * :download:`download <dataset/signature_minimal.zip>`       最小構成 (クラスタ数 = 3)
   + :download:`download <dataset/signature_multi_class.zip>` 複数クラス (クラスタ数 = 2～6)
     - :download:`download <dataset/signature_integral.zip>`  複数クラス (クラスタ数 = 2～6)、積算グラフ追加（※5）
 
| ※5 paplot付属のexampleと同等の設定

.. _conf_pmsignature:

5. pmsignature
---------------------------

 * :download:`download <dataset/pmsignature_minimal.zip>`        最小構成 (クラスタ数 = 3)
   + :download:`download <dataset/pmsignature_multi_class.zip>`  複数クラス (クラスタ数 = 2～6)（※6）
     - :download:`download <dataset/pmsignature_integral.zip>`   複数クラス (クラスタ数 = 2～6)、積算グラフ追加（※5）
   + :download:`download <dataset/pmsignature_nobackground.zip>` backgroundなし

| ※6 paplot付属のexampleと同等の設定

.. |new| image:: image/tab_001.gif
