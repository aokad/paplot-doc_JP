***************************
グラフをカスタマイズする
***************************

1. 変更方法
=======================

| 色やテキストなど、グラフの見た目はある程度変更することができます。
| グラフの見た目は2つのファイルで設定します。
| 
| 1つ目はconfigファイルです。
| 入力データに依存する要素 （グラフのバーの色や凡例、ポップアップウィンドウの文字列など）はconfigファイルで設定します。
| configファイルの記入例は以下を参照ください。
|

 - :doc:`config`
 - :doc:`config_qc` 
 - :doc:`config_sv` 
 - :doc:`config_mut` 

| 2つ目はstyleファイルです。
| 入力データに依存しない要素を設定します。
| ここでは、styleファイルについて記載します。
|

1-1. styleファイルを編集する
---------------------------------

``{paplotをインストールしたディレクトリ}/example/default.js``

このファイルをコピーして ``{paplotをインストールしたディレクトリ}/example/mystyle.js`` というファイルを作成します。

※ファイル名は任意ですが、拡張子は ``.js`` にしてください。

作成したファイルを開いて変更します。

.. note::

  色の指定はRGBもしくは色名で指定することができます。
  
  .. code-block:: javascript
  
    // RGBで指定する場合
    bar_select_color: "#1F77B4",
    // color nameで指定する場合
    bar_select_color: "red",
  
  **RGBで指定する場合**
  
  | Red → Green → Blueの順に ``00～FF`` まで、6桁の16進表記で指定し、先頭に ``#`` をつけてください。
  |
  
  **色名(カラーネーム)について**
  
  | UNIX X11カラーといい、わかりやすくするために140色に名称がついています。
  | ここで定義されている色名であれば、RGB値の代わりに指定することができます。
  | 
  | https://www.w3.org/TR/css3-color/#svg-color
  

1-2. 設定ファイルを編集する
---------------------------------

``{paplotをインストールしたディレクトリ}/example/example.cfg``

このファイルを開いて次の箇所を変更します。

スタイルファイルを今回作成したものを使用するように変更します。

.. code-block:: cfg

  [style]
  path = {paplotをインストールしたディレクトリ}/example/mystyle.js
  
  # ~/tmpにインストールした場合はこのようになる
  # ~/tmp/paplot/example/mystyle.js


1-3. 出力する
---------------------

.. code-block:: bash

  cd {paplotをインストールしたディレクトリ}
  pa_plot qc "example/qc/*.csv" ./tmp STYLE --config_file example/example.cfg


1-4. 出力されたファイルを変更する
--------------------------------------

上で作成したファイルは次のディレクトリにコピーされています。

すでにpaplotで出力したHTMLファイルを変更する場合、スタイルファイル (mystyle.js) を編集し、再読み込み(ブラウザで ``F5`` )すれば反映されます。

.. code-block:: bash

  ./tmp
    ├ STYLE
    │   ├ graph_qc.html
    │   └ graph_sv.html
    │
    ├ js
    ├ lib
    └ style
        ├ default.js     <--- デフォルト
        └ mystyle.js     <--- 今回作成したファイル


2. 設定項目
=======================

.. code-block:: javascript

  (function(){
  style_general = {
      font_family: "'Helvetica Neue', Helvetica, Arial, sans-serif",
  }
      
  // style of quality check graphs
  style_qc = {
  };

  // style of genome-wide bar plot
  style_sv_bar = {
      // title's text options
      title_top: "Genome-wide SVs identify",
      title_y: "samples with SV breakp.",
      title_x: "Chromosome",
  };

  // style of thumbnails
  style_sv_thumb = {
      // circular sector's color options
      arc_fill_opacity: 1.0,
      arc_stroke_opacity: 1.0,
      
      // link options
      link_width: "1px",
      link_opacity: 1.0,
  };

  // style of detail image (on click)
  style_sv_detail = {
      // windows header
      win_header_text_color: "#000000",
      win_header_background_color: "#CFCFCF",
      win_border_color: "#D3D3D3",
      win_border_width: "1px",
      win_background_color: "white",
      
      // circular sector's color options
      arc_fill_opacity: 1.0,
      arc_stroke_opacity: 1.0,
      
      // circular sector's label options
      arc_label_fontsize: "10px",
      arc_label_color: "#333333",
      
      // link options
      link_width: "2px",
      link_opacity: 1.0,
      
      // link(on mouse) options
      link_select_color: "#d62728",
      link_select_width: "3px",
      link_select_opacity: 1.0,
  };

  // style of mutaion-matrix
  style_mut = {
      // title's text options
      title_sample: "Sample",
      title_sample_y: "Number of mutation",
      
      title_gene: "Genes",
      title_gene_y1: "% Samples",
      title_gene_y2: "with mutation",
      
      func_title: "functions",
  };
  })();

  
透過度(opacity) について、設定値と見た目は次の通りです。

.. image:: image/link-opacity.PNG
  :scale: 100%
  
