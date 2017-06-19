**********************************************
Config 記述方法 (signature) |new|
**********************************************

----------------------------------------------------------
全設定項目
----------------------------------------------------------

.. code-block:: cfg
  
  ###################### signature
  [signature]

  # ポップアップウィンドウの表示内容
  # 詳細はページ下段の「ユーザ定義フォーマット」に記載
  tooltip_format_signature_title = {sig}
  tooltip_format_signature_partial = {route}: {#sum_item_value:6.2}
  tooltip_format_mutation_title = {id}
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
  # signatureのY軸最大値 (-1の場合、それぞれのデータの最大値を使用する)
  signature_y_max = -1
  
  # signatureのbarの色
  alt_color_CtoA = #1BBDEB
  alt_color_CtoG = #211D1E
  alt_color_CtoT = #E62623
  alt_color_TtoA = #CFCFCF
  alt_color_TtoC = #ACD577
  alt_color_TtoG = #EDC7C4
  
  # 入力フォーマット (自分のデータに合わせて変更する)
  [result_format_signature]

  # 入力形式 (現在はjsonのみ)
  format = json

  # background を使用しているかどうか
  background = True
  
  # jsonファイルのkey名
  key_id = id
  key_mutation = mutation
  key_signature = signature
  key_mutation_count = mutation_count

----------------------------------------------------------
ポップアップウィンドウの表示内容
----------------------------------------------------------

| 記載方法は :ref:`ユーザ定義フォーマット<user_format>` を参照してください。
| 
| 表示箇所ごとに4種類設定しますが、書き方は同一です。
| それぞれ次のキーワードが使用できます。
|

**tooltip_format_signature_title**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{sig}              signatureの色別グループのラベル。'C > A' や 'C > G' 等
{#sum_group_value} signatureの色別グループの合計値
================== ============================================================

**tooltip_format_signature_partial**

================== ============================================================
キーワード         解説                                                        
================== ============================================================
{route}            signatureの棒グラフ1本分のラベル。'ApCpA' や 'CpCpA' 等
{#sum_item_value}  signatureの棒グラフ1本分の値
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

  # signature - タイトル
  tooltip_format_signature_title = {sig}
  
  # signature - 各項目
  tooltip_format_signature_partial = {route}: {#sum_item_value:6.2}
  
  # 積み上げグラフ - タイトル
  tooltip_format_mutation_title = {id}
  
  # 積み上げグラフ - signatureごと
  tooltip_format_mutation_partial = {sig}: {#sum_item_value:.2}
  
.. image:: image/conf_sig1.PNG
  :scale: 100%
  
.. |new| image:: image/tab_001.gif
