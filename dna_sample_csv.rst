========================================
DNA Sample_conf.csvの書き方
========================================

項目は6種類あります。

+-----------------+---------------------------------------------------+
| [fastq]         | FASTQファイルを入力として解析します               |
+-----------------+---------------------------------------------------+
| [bam_tofastq]   | BAMを入力してFASTQファイルに戻してから解析します  |
+-----------------+---------------------------------------------------+
| [bam_import]    | 入力したBAMを再アライメントせずに解析を実行します |
+-----------------+---------------------------------------------------+
| [mutation_call] | 変異Callが実行されます                            |
+-----------------+---------------------------------------------------+
| [sv_detection]  | SV検出が実行されます                              |
+-----------------+---------------------------------------------------+
| [controlpanel]  | controlパネルのペアを指定します                   |
+-----------------+---------------------------------------------------+
| [summary]       | BamSummaryを出力します                            |
+-----------------+---------------------------------------------------+

| DNA解析では
| [fastq], [bam_tofastq], [bam_import] は入力ファイルの情報を記載します．
| [mutation_call], [sv_detection], [controlpanel], [summary] には解析するための情報を記載します．
|

[fastq]の記載方法
^^^^^^^^^^^^

| 項目[fastq]にはinput fastqファイルのパスを記載します．

.. code-block:: bash

  # サンプル名,read1.fastq,read2.fastq  と記載します（カンマ区切りです）
  sample1_tumor,/home/genomon/sample1_T_read1.fastq,/home/genomon/sample1_T_read2.fastq
  sample1_normal,/home/genomon/sample1_N_read1.fastq,/home/genomon/sample1_N_read2.fastq

| サンプル名は任意で指定してください。ディレクトリやファイル名で使用されます。
| 

[bam_import]の記載方法
^^^^^^^^^^^^

| 項目[bam_import]にはinput bamファイルのパスを記載します．

.. code-block:: bash

  # サンプル名,bam  と記載してください（カンマ区切りです）
  sample3_tumor,/home/genomon/sample3_T.bam
  
| bam indexファイル(.bai)がセットで必要です。
| 

[mutation_call],[sv_detection]の記載方法
^^^^^^^^^^^^

| 項目[mutation_call][sv_detection]にはtumorとnormalのペア情報を記載します．
| normalのコントロールパネルを作る場合は、そちらも記載します．

.. code-block:: bash

  # Tumorサンプル名,Normalサンプル名,Controlパネル名 と記載してください．

  # パターン１：tumorとnormalのペアのサンプルで、コントロールパネルがある場合
  # tumorサンプル名,normalサンプル名,コントロールパネル名 と記載してください。コントロールパネル名は項目[control_panel]で定義した名前を使用します。
  sample1_tumor,sample1_normal,Panel1
  
  # パターン２：tumorとnormalのペアのサンプルで、コントロールパネルがない場合
  # tumorサンプル名,normalサンプル名,None と記載してください。
  sample1_tumor,sample1_normal,None
  
  # パターン３：tumorだけで、normalのペアのサンプルがない。コントロールパネルがある場合
  # tumorサンプル名,None,コントロールパネル名 と記載してください。
  sample3_tumor,None,Panel1

  # パターン４：tumorだけで、normalのペアのサンプルがない。コントロールパネルがない場合
  # tumorサンプル名,None,None と記載してください。
  sample4_tumor,None,None

| この項目に定義するサンプル名は[fastq], [bam_tofastq], [bam_import]のいずれかで定義されていなくてはなりません．
| 

[controlpanel]の記載方法
^^^^^^^^^^^^

項目[controlpanel]には、normalのサンプル名を複数指定して、panel名を付けてnormalサンプルの集まりとして指定します．

.. code-block:: bash

  # panel名,normalサンプル1,normalサンプル2,normalサンプル3,・・・,normalサンプルNと記載してください。
  panel1,sample1_normal,sample2_normal,sample3_normal,sample4_normal
  panel2,sample5_normal,sample6_normal,sample7_normal,sample8_normal
  
| 指定するサンプル数Nに最大値はないです。
| サンプル名は[fastq], [bam_tofastq], [bam_import]のいずれかで定義されていなくてはなりません．
| パネル名は任意で指定してください。
| 

[summary]の記載方法
^^^^^^^^^^^^

項目[summary]にはサンプル名を記載します．

.. code-block:: bash

  # ペアで記載する必要はありません。summary出力するサンプル名を記載してください
  sample1_normal
  sample2_normal
  sample3_normal
  sample1_tumor
  sample2_tumor
  sample3_tumor


| この項目に定義するサンプル名は[fastq], [bam_tofastq], [bam_import]のいずれかで定義されていなくてはなりません．
| 
