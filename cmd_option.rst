# コマンドオプション

Description 

.. code-block:: bash
  pa_plot {qc, sv} [-h] [--version] [--config_file CONFIG_FILE]
                  input output_dir project_name

 - `{qc, sv}`
 
    Sub commands

 - `input`

    Input data files,<br>
    Use wildcard('*') to specify multiple files, and take `"` last and first.

 - `output_dir`

    output directory path,<br>
    see following section.

 - `project_name`
 
   project name,<br>
   it is output html's title.

 - `--config_file` 

    configure file,<br>
    if not specified, use the default.
