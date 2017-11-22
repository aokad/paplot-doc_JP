************************
はじめに
************************

Automatic generation of cancer genome interactive report via paplot
------------------------------------------------------------------------

| paplot はゲノム解析結果を自動でグラフ化するツールです。

.. image:: image/mutation_list.PNG
  :scale: 100%

| paplot は皆さんのゲノム解析を少しだけ楽にする…かもしれません。
|

作成できるレポートの種類
----------------------------

1. Quality Control (QC) レポート

アライメント率やカバレッジ率など、シーケンスデータの品質を表示します。

.. image:: image/qc_dummy.PNG
  :scale: 100%

2. Chromosomal Aberration (CA) レポート

構造異常や融合遺伝子など、染色体間の変異を円形のプロットで可視化し、棒グラフでその分布を表示します。

.. image:: image/sv_dummy.PNG
  :scale: 100%

3. Mutation Matrix レポート

検出した変異について縦軸を遺伝子 (Gene)、横軸をサンプル (Sample) として、変異タイプ別に表示します。

.. image:: image/mut_dummy.PNG
  :scale: 100%

4. Mutational Signature レポート

検出した変異についての特徴的なパターン (変異シグネチャ) を表示します。

.. image:: image/sig_dummy.PNG
  :scale: 100%

`pmsignature <https://github.com/friend1ws/pmsignature/>`_ を使用した表現も可能です。

.. image:: image/pmsig_dummy.PNG
  :scale: 100%

.. |new| image:: image/tab_001.gif
