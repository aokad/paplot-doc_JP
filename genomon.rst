**************************
Genomon データを使用する
**************************

Genomo-pipeline に関しては、各バージョンの設定ファイルを用意しています。

※カスタマイズする場合は :doc:`config` を参照して変更してください。


``{paplotをインストールしたディレクトリ}/config_template``

====================================== ===============================
file name                              version
====================================== ===============================
genomon_v2_0_0.cfg                     Genomon 2.0.0 ～ 2.0.3 
genomon_v2_0_5_v2_0_4.cfg              Genomon 2.0.4 ～ 2.0.5
genomon_v2_2_0_merge.cfg               Genomon 2.2.0
genomon_v2_3_0_merge.cfg               Genomon 2.3.0
genomon_v2_4_0_dna_merge.cfg           Genomon 2.4.0 (dna)
genomon_v2_4_0_rna_merge.cfg           Genomon 2.4.0 (rna)
====================================== ===============================

※ Genomon 2.4.0 よりrna結果のpaplot出力に対応しました。

Genomon-pipeline の結果ファイルをもとにしたバージョンの見分け方

============================= ================== ================= =============== ==================
version                       mutation           sv                qc              post-analysis
============================= ================== ================= =============== ==================
Genomon 2.0.0 ～ 2.0.3        ヘッダなし         ヘッダなし        結果なし        結果なし
Genomon 2.0.4 ～ 2.0.5        ヘッダあり         ヘッダなし        結果あり        結果なし
Genomon 2.2.0                 ヘッダあり         ヘッダあり        結果あり        結果あり
============================= ================== ================= =============== ==================

※genomon 2.3.0 以降はpaplot/{サンプルファイル名}/index.html にGenomon-pipeline のバージョン名を出力しています。

実行例

.. code-block:: bash

  genomon_root={Genomonを実行したディレクトリ}
  sample={Genomon実行時のサンプルファイル名のディレクトリ}
  output_dir={paplotの出力ディレクトリ}
  project_name={プロジェクト名}
  paplot_install_dir={paplotをインストールしたディレクトリ}
  
  # for Genomon 2.4.0
  ## dna
  pa_plot qc ${genomon_root}/post_analysis/${sample}/merge_qc.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_4_0_dna_merge.cfg
  pa_plot sv ${genomon_root}/post_analysis/${sample}/merge_sv_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ./config_template/genomon_v2_4_0_dna_merge.cfg
  pa_plot mutation ${genomon_root}/post_analysis/${sample}/merge_mutation_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ./config_template/genomon_v2_4_0_dna_merge.cfg
  
  ## rna
  pa_plot qc ${genomon_root}/post_analysis/${sample}/merge_starqc.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_4_0_rna_merge.cfg
  pa_plot sv ${genomon_root}/post_analysis/${sample}/merge_fusionfusion_filt.txt ${output_dir} ${project_name} --config_file ./config_template/genomon_v2_4_0_rna_merge.cfg
  
  # for Genomon 2.3.0
  pa_plot qc ${genomon_root}/post_analysis/${sample}/merge_qc.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_3_0_merge.cfg
  pa_plot sv ${genomon_root}/post_analysis/${sample}/merge_sv_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ./config_template/genomon_v2_3_0_merge.cfg
  pa_plot mutation ${genomon_root}/post_analysis/${sample}/merge_mutation_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ./config_template/genomon_v2_3_0_merge.cfg

  # for Genomon 2.2.0
  pa_plot qc ${genomon_root}/post_analysis/${sample}/merge_qc.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_2_0_merge.cfg
  pa_plot sv ${genomon_root}/post_analysis/${sample}/merge_sv_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_2_0_merge.cfg
  pa_plot mutation ${genomon_root}/post_analysis/${sample}/merge_mutation_filt_pair_controlpanel.txt ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_2_0_merge.cfg

  # for Genomon 2.0.4 or Genomon 2.0.5
  pa_plot qc "${genomon_root}/summary/*/*.tsv" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_5_v2_0_4.cfg
  pa_plot sv "${genomon_root}/sv/*/*.genomonSV.result.txt" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_5_v2_0_4.cfg
  pa_plot mutation "${genomon_root}/mutation/*/*_genomon_mutations.result.txt" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_5_v2_0_4.cfg

  # for Genomon 2.0.0 ～ 2.0.3
  pa_plot sv "${genomon_root}/sv/*/*.genomonSV.result.txt" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_0.cfg
  pa_plot mutation "${genomon_root}/mutation/*/*_genomon_mutations.result.txt" ${output_dir} ${project_name} --config_file ${paplot_install_dir}/config_template/genomon_v2_0_0.cfg

