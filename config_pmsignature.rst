**********************************************
Config 記述方法 (pmsignature) |new|
**********************************************

----------------------------------------------------------
全設定項目
----------------------------------------------------------

.. code-block:: cfg
  
  ###################### pmsignature
  [pmsignature]

  # ポップアップウィンドウの表示内容
  # 詳細はページ下段の「ユーザ定義フォーマット」に記載
  tooltip_format_ref1 = A: {a:.2}
  tooltip_format_ref2 = C: {c:.2}
  tooltip_format_ref3 = G: {g:.2}
  tooltip_format_ref4 = T: {t:.2}
  tooltip_format_alt1 = C -> A: {ca:.2}
  tooltip_format_alt2 = C -> G: {cg:.2}
  tooltip_format_alt3 = C -> T: {ct:.2}
  tooltip_format_alt4 = T -> A: {ta:.2}
  tooltip_format_alt5 = T -> C: {tc:.2}
  tooltip_format_alt6 = T -> G: {tg:.2}
  tooltip_format_strand = + {plus:.2} - {minus:.2}
  tooltip_format_mutation_title = {id}
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
  # pmsignatureのboxの色
  color_A = #06B838
  color_C = #609CFF
  color_G = #B69D02
  color_T = #F6766D
  color_plus = #00BEC3
  color_minus = #F263E2
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  [result_format_pmsignature]

  # 入力形式 (現在はjsonのみ)
  format = json

  # background を使用しているかどうか
  background = True

  # jsonファイルのkey名
  key_id = id
  key_mutation = mutation
  key_ref = ref
  key_alt = alt
  key_strand = strand
  key_mutation_count = mutation_count
  
----------------------------------------------------------
ポップアップウィンドウの表示内容
----------------------------------------------------------

| 記載方法は :ref:`ユーザ定義フォーマット<user_format>` を参照してください。
| 
| 表示箇所ごとに4種類設定しますが、書き方は同一です。
| それぞれ次のキーワードが使用できます。
|

**tooltip_format_ref* (pmsignature 下段の5つのbox)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{a}                Aの値
{c}                Cの値
{g}                Gの値
{t}                Tの値
================== ============================================================

**tooltip_format_alt* (pmsignature 上段の1つのbox)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{ca}               C->Aの値
{cg}               C->Gの値
{ct}               C->Tの値
{ta}               T->Aの値
{tc}               T->Cの値
{tg}               T->Gの値
================== ============================================================

**tooltip_format_strand**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{plus}             プラスの値
{minus}            マイナスの値
================== ============================================================

**tooltip_format_mutation_title (積み上げグラフ)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{id}               `key_id` で入力したサンプル名です。
{#sum_mutaion_all} 全mutation数
================== ============================================================

**tooltip_format_mutation_partial (積み上げグラフ)**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{sig}              signature名 "Signature {signature番号}" で表示します。
{#sum_item_value}  積み上げグラフの合計値
================== ============================================================

**デフォルトでの設定内容と表示との対応**

.. code-block:: cfg

  # pmsignature - 下段の5つのbox
  tooltip_format_ref1 = A: {a:.2}
  tooltip_format_ref2 = C: {c:.2}
  tooltip_format_ref3 = G: {g:.2}
  tooltip_format_ref4 = T: {t:.2}

  # pmsignature - 上段のbox
  tooltip_format_alt1 = C -> A: {ca:.2}
  tooltip_format_alt2 = C -> G: {cg:.2}
  tooltip_format_alt3 = C -> T: {ct:.2}
  tooltip_format_alt4 = T -> A: {ta:.2}
  tooltip_format_alt5 = T -> C: {tc:.2}
  tooltip_format_alt6 = T -> G: {tg:.2}

  # pmsignature - strand
  tooltip_format_strand = + {plus:.2} - {minus:.2}
  
  # 積み上げグラフ - タイトル
  tooltip_format_mutation_title = {id}
  
  # 積み上げグラフ - signatureごと
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
.. image:: image/conf_pmsig1.PNG
  :scale: 100%

.. |new| image:: image/tab_001.gif
