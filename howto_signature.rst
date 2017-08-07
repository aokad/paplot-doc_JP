=============================
Mutaitonal Signature レポート
=============================

Mutaitonal Signature レポートでは検出した変異についての特徴的なパターン (変異シグネチャ) を表示します。

:上段 (Signature):
  変異シグネチャを表示します。

:下段 (寄与度グラフ):
  サンプルごとの変異について、変異シグネチャの寄与度を表示します。

.. image:: image/sig_dummy.PNG
  :scale: 100%

また、積み上げグラフの下のリストボックスにより表示モードを切り替えることができます。

:view mode:
  - rate ... 変異の数を1としたときのsignatureの割合を % で表示します。
  - integral ... 実際の変異数に対する割合を表示します。

:sort by:
  - sampleID ... サンプルID順
  - mutation count ... 変異数の降順

  view modeがintegralの場合のみ、ソート方法を選択できます。


「view mode」で「integral」を選択し、「sort by」で「mutation count」を選択した場合の表示例

.. image:: image/sig_operation1.PNG
  :scale: 100%

pmsignatureについても同様です。

.. image:: image/pmsig_dummy.PNG
  :scale: 100%

.. |new| image:: image/tab_001.gif