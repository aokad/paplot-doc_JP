************************
はじめに
************************

| paplotはゲノム解析結果を自動でグラフ化するツールです。
|
| ゲノムを解析して、このようなテキストファイルができたとします。
|

.. image:: image/mutation_list.PNG
  :scale: 100%

| このあと何をしますか？
| グラフを作成しないでしょうか？
| 毎回手動で作成したり、似たようなスクリプトを書いていたりしないでしょうか？
| データの抽出条件、ソート条件を変えて再度グラフを作成していないでしょうか？
|
| paplotはこの作業を自動化して、皆さんのゲノム解析を少しだけ楽にする…かもしれません。
|

作成できるグラフ
-------------------

1. QC (Quality Control) グラフ

bamファイルの品質をグラフに表示します。

.. image:: image/qc_dummy.png
  :scale: 100%

2. CA (Chromosomal Aberration) グラフ

Structural Variation (SV) 等、Chromosome間の変異を円形のplotで可視化し、棒グラフでその分布を表示します。

.. image:: image/sv_dummy.png
  :scale: 100%

3. mutation-matrix グラフ

検出したmutation について縦軸を遺伝子(Gene), 横軸をサンプル(Sample) として、変異タイプ別に表示します。

.. image:: image/mut_dummy.png
  :scale: 100%

