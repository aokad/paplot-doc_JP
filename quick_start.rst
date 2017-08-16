*****************
クイックスタート
*****************

#. paplot をインストール
#. サンプルデータでコマンドを実行
#. 結果ファイルを表示

1. paplot をインストール
---------------------------

| paplot は python2.7 および python 3.5 で動作確認しています。
| また、paplot は追加パッケージを必要としません。
| より詳しいインストール手順は :doc:`install` を参照してください。

.. code-block:: bash

  cd {インストールしたいディレクトリ}
  # v0.5.3の場合
  wget https://github.com/Genomon-Project/paplot/archive/v0.5.3.zip
  unzip v0.5.3.zip
  cd paplot-0.5.3/

  python setup.py build install

| 正しくインストールされたか確認します。

**インストールの確認**

| 以下を入力してください。

.. code-block:: bash

  paplot conf

| このように表示されればインストール成功です。

.. code-block:: bash

  **********************
     hello paplot !!!
  **********************
  
  config file:/usr/lib/python2.7/site-packages/{paplot-versoion}-py2.7.egg/config/paplot.cfg
  (このあとにデフォルト設定の内容が表示されます)


2. サンプルデータでコマンドを実行
-------------------------------------

| paplot はコマンドから使用します。
| 
| 基本的な使い方は次の通りです。
| 詳細なオプションは :doc:`command` を参照してください。

.. code-block:: bash

  paplot subcommand [--config_file CONFIG_FILE] [--title TITLE]
                    [--ellipsis ELLIPSIS] [--overview OVERVIEW]
                    [--remarks REMARKS]
                    input output_dir project_name

|

**必ず入力する項目**

:subcommand:
  paplot のサブコマンドです。いずれかを選択します。
  
  - qc
  - ca
  - mutation
  - signature
  - pmsignature

:input:
  入力ファイルです。

:output_dir:
  出力ディレクトリを指定します。ディレクトリ構成は次の章を参照してください。

:project_name:
  プロジェクト名です。出力ファイルのタイトルに使用します。

サンプルデータを用意していますので実行します。

.. code-block:: bash

  cd {paplotをインストールしたディレクトリ}

  # QC レポート
  paplot qc example/qc_brush/data.csv ./tmp demo

  # Chromosomal Aberration レポート
  paplot ca example/ca_option/data.csv ./tmp demo

  # Mutation Matrix レポート
  paplot mutation example/mutation_option/data.csv ./tmp demo

  # Mutational Signatureレポート
  paplot signature "example/signature_stack/data*.json" ./tmp demo

  # pmsignature レポート
  paplot pmsignature "example/pmsignature_stack/data*.json" ./tmp demo


3. 結果ファイルを表示
------------------------

HTML ファイルができていますか？

.. code-block:: bash

  {output_dir} で指定したディレクトリ
    ├ demo
    │   ├ graph_ca.html            <--- Chromosomal Aberration レポート
    │   ├ graph_mut.html           <--- Mutation Matrix レポート
    │   ├ graph_pmsignature2.html  <--- pmsignature レポート (数字は変異シグネチャの数)
    │   ├ graph_pmsignature3.html
    │   ├ graph_pmsignature4.html
    │   ├ graph_pmsignature5.html
    │   ├ graph_pmsignature6.html
    │   ├ graph_qc.html            <--- QC レポート
    │   ├ graph_signature2.html    <--- Mutational Signature レポート (数字は変異シグネチャの数)
    │   ├ graph_signature3.html
    │   ├ graph_signature4.html
    │   ├ graph_signature5.html
    │   └ graph_signature6.html
    │
    ├ js          <--- この4つのディレクトリはHTMLファイルを表示するために必要です。消さないでください。
    ├ layout
    ├ lib
    ├ style
    │
    └ index.html             <--- このファイルをウェブブラウザで開いてください。


| index.html ファイルをウェブブラウザで開いてください。
|
| ※ HGC スパコン等、サーバ上で実行した場合はファイルをローカルに転送するか、NoMachime 等サーバ上の仮想ウィンドウで表示してください。
|   ローカルに転送する場合は、:file:`tmp` ディレクトリを丸ごとコピーしてください。
| 
| 次のように見えていますか?
| 
| **QC レポート**

.. image:: image/qc_dummy.PNG
  :scale: 100%

| **Chromosomal Aberration レポート**

.. image:: image/sv_dummy.PNG
  :scale: 100%

| **Mutation Matrix レポート**

.. image:: image/mut_dummy.PNG
  :scale: 100%

| **Mutational Signature レポート**

.. image:: image/sig_dummy.PNG
  :scale: 100%

| **pmsignature レポート**

.. image:: image/pmsig_dummy.PNG
  :scale: 100%

| それぞれのレポートの使い方は `HOW TO USE GRAPHS <./index.html#how-to-toc>`_ を参照してください。
|

.. |new| image:: image/tab_001.gif
