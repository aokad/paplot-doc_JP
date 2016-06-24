**************************
Genomonデータを使用する
**************************

| Genomonに関しては、各バージョンの設定ファイルを用意しています。
| ※カスタマイズする場合は :doc:`config` を参照して変更してください。
|

``{paplotをインストールしたディレクトリ}/config_template``

| Genomonの結果ファイルをもとにしたバージョンの見分け方
|

============================= ================== ================= =============== ==================
version                       mutation           sv                qc              post-analysis
============================= ================== ================= =============== ==================
Genomon 2.0.5 もしくは 2.0.4  ヘッダあり         ヘッダなし        結果あり        結果なし
Genomon 2.2.0                 ヘッダあり         ヘッダあり        結果あり        結果あり
============================= ================== ================= =============== ==================

| ※ Genomon 2.3.0以降は実行時のconfigファイルにバージョンの記載があります。
|

実行例

.. code-block:: bash

  genomon_root={Genomonを実行したディレクトリ}
  sample={Genomon実行時のサンプルファイル名のディレクトリ}
  output_dir={paplotの出力ディレクトリ}
  project_name={プロジェクト名}
  paplot_install_dir={paplotをインストールしたディレクトリ}
  
  # for Genomon 2.3.0

  pa_plot qc ${genomon_root}/post_analysis/${sample}/merge_qc.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_3_0_merge.cfg
  pa_plot sv ${genomon_root}/post_analysis/ACC_000/merge_sv_filt_pair_controlpanel.txt ./ACC_230_m ACC --config_file ./config_template/genomon_v2_3_0_merge.cfg
  pa_plot mutation ${genomon_root}/post_analysis/ACC_000/merge_mutation_filt_pair_controlpanel.txt ./ACC_230_m ACC --config_file ./config_template/genomon_v2_3_0_merge.cfg

  # for Genomon 2.2.0

  pa_plot qc ${genomon_root}/post_analysis/${sample}/merge_qc.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_2_0_merge.cfg
  pa_plot sv ${genomon_root}/post_analysis/${sample}/merge_sv_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_2_0_merge.cfg
  pa_plot mutation ${genomon_root}/post_analysis/${sample}/merge_mutation_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_2_0_merge.cfg

  # for Genomon 2.0.5 or Genomon 2.0.4
  pa_plot qc "${genomon_root}/summary/*/*.tsv" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_5_v2_0_4.cfg
  pa_plot sv "${genomon_root}/sv/*/*.genomonSV.result.txt" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_5_v2_0_4.cfg
  pa_plot mutation "${genomon_root}/mutation/*/*_genomon_mutations.result.txt" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_5_v2_0_4.cfg


