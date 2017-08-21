***************************
グラフをカスタマイズする
***************************

1. 変更方法
=======================

| 色やテキストなど、グラフの見た目はある程度変更することができます。
| グラフの見た目は 2 つのファイルで設定します。
| 
| 1 つ目は設定ファイルです。
| グラフのバーの色や凡例、ポップアップの文字列のように入力データに依存する要素は設定ファイルで設定します。
| 設定ファイルの記入例は以下を参照ください。

[入門編]

 - :doc:`data_mat` 
 - :doc:`data_qc` 
 - :doc:`data_ca` 
 - :doc:`data_signature` 
 - :doc:`data_pmsignature` 

[上級者向け]

 - :doc:`config`

| 2 つ目は style ファイルです。
| 入力データに依存しない要素を設定します。
| ここでは、style ファイルについて記載します。
|

1-1. style ファイルを編集する
---------------------------------

デフォルトの style ファイルはここにあります。

``{paplot をインストールしたディレクトリ}/example/default.js``

このファイルをコピーして 新しい style ファイルを作成します。

ここでは、例としてこのように作成します。 ``{paplotをインストールしたディレクトリ}/example/mystyle.js``

ファイル名は任意ですが、拡張子は ``.js`` にしてください。

作成したファイルを開いて変更します。

.. note::

  色の指定は RGB もしくは色名で指定することができます。
  
  .. code-block:: javascript
  
    // RGB で指定する場合
    bar_select_color: "#1F77B4",
    
    // 色名で指定する場合
    bar_select_color: "red",
  
  **RGB で指定する場合**
  
  | Red → Green → Blue の順に ``00～FF`` まで、6 桁の 16 進表記で指定し、先頭に ``#`` をつけてください。
  |
  
  **色名について**
  
  | UNIX X11 カラーともいい、わかりやすくするために 140 色に名称がついています。
  | ここで定義されている色名であれば、RGB 値の代わりに指定することができます。
  | 
  | https://www.w3.org/TR/css3-color/#svg-color
  

1-2. 設定ファイルを編集する
---------------------------------

今回作成したスタイルファイルを使用するように設定ファイルを変更します。

``{paplot をインストールしたディレクトリ}/example/example.cfg``

このファイルを開いて次の箇所を変更します。

.. code-block:: cfg

  [style]
  path = {paplot をインストールしたディレクトリ}/example/mystyle.js
  
  # ~/tmp にインストールした場合はこのようになる
  # ~/tmp/paplot/example/mystyle.js


1-3. paplot を実行する
----------------------------------

.. code-block:: bash

  cd {paplot をインストールしたディレクトリ}
  paplot qc "example/qc/*.csv" ./tmp style_test --config_file example/example.cfg


1-4. 出力されたファイルを変更する
--------------------------------------

上で作成したファイルは次のディレクトリにコピーされています。

すでに paplot で出力した HTML ファイルを変更する場合、スタイルファイル (mystyle.js) を編集し、再読み込み (ウェブブラウザで ``F5``) すれば反映されます。

.. code-block:: bash

  ./tmp
    ├ style_test
    │   └ graph_qc.html
    │
    ├ js
    ├ layout
    ├ lib
    └ style
        ├ default.js     <--- デフォルト
        └ mystyle.js     <--- 今回作成したファイル


2. 設定項目
=======================

.. code-block:: javascript

  // ----------------------------------------
  // 共通
  // ----------------------------------------
  (function(){
  style_general = {
      font_family: "'Helvetica Neue', Helvetica, Arial, sans-serif",
  }
  
  // ----------------------------------------
  // QC レポート
  // ----------------------------------------
  style_qc = {
  
      // 領域選択用グラフ
      // Y 方向ボーダーライン
      brush_border_y_color: "#DDDDCC",
      brush_border_y_opacity: 0.5,
      
      // 通常グラフ
      // Y 方向ボーダーライン
      plot_border_y_color: "#DDDDCC",
      plot_border_y_opacity: 0.2,
      
      // Y 軸ラベル
      title_y_font_size: "12px",
      
      // 凡例
      legend_title_font_size: "16px",
      legend_text_font_size: "12px",
  };
  
  // ----------------------------------------
  // Chromosomal Aberration レポート
  // ----------------------------------------
  
  // 横長の棒グラフ
  style_sv_bar = {

      // X 軸ラベル
      title_x: "Chromosome",
      title_x_font_size: "14px",
      axis_x_font_size: "9px",
      
      // Y 軸ラベル
      title_y: "Mutations with CA breakp.",
      title_y_font_size: "12px",
      
      // 凡例
      legend_title: "Genome-wide CAs identify",
      legend_title_font_size: "16px",
      legend_text_font_size: "12px",
      
      // X 方向ボーダーライン
      border_x_main_color: "#E0E0E0",
      border_x_main_width: "1px",
      border_x_sub_color: "#A6A6A6",
      border_x_sub_width: "1px",
      
      // Y 方向ボーダーライン
      border_y_color: "#DDDDCC",
      border_y_opacity: 0.5,
  };
  
  // 円形のプロット
  style_sv_thumb = {

      // 円の弧 (fill: 塗りつぶし色, stroke: 枠線色)
      arc_fill_opacity: 1.0,
      arc_stroke_opacity: 1.0,
      
      // 切断点をつなぐ曲線
      link_width: "1px",
      link_opacity: 1.0,
  };
  
  // 円形のプロット (クリックで表示される方)
  style_sv_detail = {

      // 表示ウィンドウ
      win_header_text_color: "#000000",
      win_header_background_color: "#CFCFCF",
      win_border_color: "#D3D3D3",
      win_border_width: "1px",
      win_background_color: "white",
      
      // 円の弧  (fill: 塗りつぶし色, stroke: 枠線色)
      arc_fill_opacity: 1.0,
      arc_stroke_opacity: 1.0,
      
      // 円の弧のラベル
      arc_label_fontsize: "10px",
      arc_label_color: "#333333",
      
      // 切断点をつなぐ曲線
      link_width: "2px",
      link_opacity: 1.0,
      
      // 切断点をつなぐ曲線 (マウスを乗せた時)
      link_select_color: "#d62728",
      link_select_width: "3px",
      link_select_opacity: 1.0,
  };

  // ----------------------------------------
  // Mutaion Matrix レポート
  // ----------------------------------------
  style_mut = {
  
      // -------------------------
      // 横長のグラフ (サンプル)
      // -------------------------
      // タイトル
      title_sample: "Sample",
      title_sample_font_size: "14px",
      
      // Y 軸ラベル
      title_sample_y: "Number of mutation",
      title_sample_y_font_size: "12px",
      
      // X 方向ボーダーライン
      virtical_border_x_color: "#CCCCEE",
      virtical_border_x_width: "1px",
      
      // Y 方向ボーダーライン
      virtical_border_y_color: "#DDDDCC",
      virtical_border_y_opacity: 0.5,

      // -------------------------
      // 縦長のグラフ (遺伝子)
      // -------------------------
      // タイトル
      title_gene: "Genes",
      title_gene_font_size: "14px",
      
      // Y 軸ラベル
      title_gene_y1: "% Samples",
      title_gene_y2: "with mutations",
      title_gene_y1_font_size: "12px",
      title_gene_y2_font_size: "12px",
      
      // X 方向ボーダーライン
      horizon_border_x_color: "#CCCCEE",
      horizon_border_x_width: "1px",
      
      // Y 方向ボーダーライン
      horizon_border_y_color: "#DDDDCC",
      horizon_border_y_opacity: 0.5,
      
      // 凡例
      legend_title: "Mutation type",
      legend_title_font_size: "16px",
      legend_text_font_size: "12px",
      
      // 遺伝子名
      gene_text_font_size: "9px",
      
      // -------------------------
      // サブプロット
      // -------------------------
      // X 方向ボーダーライン
      sub_border_color: "#FFFFFF",
      sub_border_width: "1px",
      
  };
  
  // ----------------------------------------
  // Mutational Signature レポート
  // ----------------------------------------
  style_signature = {
  
      // -------------------------
      // 寄与度グラフ (Count)
      // -------------------------
      // タイトル
      title_integral: "Signature contribution",
      title_integral_font_size: "16px",
      
      // Y 軸ラベル
      title_integral_y: "Count",
      title_integral_y_font_size: "12px",
      
      // 凡例
      legend_integral_title_font_size: "16px",
      legend_integral_text_font_size: "12px",

      // -------------------------
      // 寄与度グラフ (Rate)
      // -------------------------
      // タイトル
      title_rate: "Signature contribution",
      title_rate_font_size: "16px",
      
      // Y 軸ラベル
      title_rate_y: "Rate",
      title_rate_y_font_size: "12px",
      
      // 凡例
      legend_rate_title_font_size: "16px",
      legend_rate_text_font_size: "12px",
      
      // -------------------------
      // 寄与度グラフ (共通)
      // -------------------------
      // Y 方向ボーダーライン
      plot_border_y_color: "#DDDDCC",
      plot_border_y_opacity: 0.5,
      
      // -------------------------
      // 変異シグネチャ
      // -------------------------
      // 変異シグネチャ名
      signature_title_font_size: "12px",
      
      // Y 軸ラベル
      signature_title_y: "Probaility",
      signature_title_y_font_size: "12px",
      
      // X 軸ラベル
      signature_title_x_font_size: "12px",
      
      // Y 方向ボーダー
      border_y_color: "#DDDDCC",
      border_y_opacity: 0.5,
  };

  // ----------------------------------------
  // pmsignature レポート
  // ----------------------------------------
  style_pmsignature = {

      // -------------------------
      // 寄与度グラフ (Count)
      // -------------------------
      // タイトル
      title_integral: "Signature contribution",
      title_integral_font_size: "16px",
      
      // Y 軸ラベル
      title_integral_y: "Count",
      title_integral_y_font_size: "12px",
      
      // 凡例
      legend_integral_title_font_size: "16px",
      legend_integral_text_font_size: "12px",
      
      // -------------------------
      // 寄与度グラフ (Rate)
      // -------------------------
      // タイトル
      title_rate: "Signature contribution",
      title_rate_font_size: "16px",
      
      // Y 軸ラベル
      title_rate_y: "Rate",
      title_rate_y_font_size: "12px",
      
      // 凡例
      legend_rate_title_font_size: "16px",
      legend_rate_text_font_size: "12px",
      
      // -------------------------
      // 寄与度グラフ (共通)
      // -------------------------
      // Y 方向ボーダーライン
      plot_border_y_color: "#DDDDCC",
      plot_border_y_opacity: 0.5,
      
      // -------------------------
      // 変異シグネチャ
      // -------------------------
      // 変異シグネチャ名
      signature_title_font_size: "12px",

      // 各ボックスのラベル
      signature_alt_font_size: "10px",
      signature_ref_font_size: "10px",
      signature_strand_font_size: "10px",

  };
  })();

| 透過度 (opacity) について、設定値と見た目は次の通りです。
| 0~1 の間で設定することができ、0 で透明、1 で不透明となります。

.. image:: image/link-opacity.PNG
  :scale: 100%
  
.. |new| image:: image/tab_001.gif
