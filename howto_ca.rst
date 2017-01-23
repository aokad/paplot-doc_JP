==============
CA グラフ
==============

| CA (Chromosomal Aberration) グラフではStructural Variation (SV) 等、Chromosome間の変異を円形のplotで可視化し、棒グラフでその分布を表示します。
| 

* 棒グラフでは全サンプルでbreakpointを集計した数を表示します。
* 円形のplotでは、サンプルごとにbreakpoint1と2を線でつないで表示します。

| 棒グラフを選択すると選択されたgenome領域にbreakpointを持つサンプルが選択されます。
| 選択方法は「ハイライト」と「選択したもののみ表示（他を隠す）」の2とおりあり、先頭のオプションボタンで選択できます。
|

.. image:: image/sv_operation1.PNG
  :scale: 100%


| 棒グラフのstackは2つあり、2つのbreak pointがchromosome を超えているか、もしくは同一 chromosome 内かで色を分けています。
| チェックを外すと、その要素は表示されません。
|

.. image:: image/sv_operation2.PNG
  :scale: 100%

| サンプルごとの円形のグラフをクリックすると拡大表示します。
| breakpointをつなぐ線の上にマウスを乗せると詳細を表示します。
|

.. image:: image/sv_operation3.PNG
  :scale: 100%
