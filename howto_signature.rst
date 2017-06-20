========================
signature レポート
========================

signature レポートでは検出したmutation についてsignatureとその集積を積み上げグラフで表示します。

:signature:
  signatureを表示します。

:積み上げグラフ:
  サンプルごとmutationについて、signatureの割合を表示します。

.. image:: image/sig_dummy.PNG
  :scale: 100%

また、積み上げグラフの下のリストボックスにより表示モードを切り替えることができます。

:view mode:
  - rate ... mutationの数を1としたときのsignatureの割合を % で表示します。
  - integral ... 実際のmutation数に対する割合を表示します。

:sort by:
  - sampleID ... サンプルID順
  - mutation count ... mutation数の降順

  view modeがintegralの場合のみ、ソート方法を選択できます。


view mode 「integral」, sort by 「mutation count」の表示例

.. image:: image/sig_operation1.PNG
  :scale: 100%

pmsignatureについても同様です。

.. image:: image/pmsig_dummy.PNG
  :scale: 100%

.. |new| image:: image/tab_001.gif