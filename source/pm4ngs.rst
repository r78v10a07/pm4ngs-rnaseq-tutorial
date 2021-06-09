.. _pm4ngs:

PM4NGS for RNA-Seq data analysis
================================

Read PM4NGS published manuscript in GIGAScience_

.. _GIGAScience: https://academic.oup.com/gigascience/article/10/1/giaa141/6067195

Sample Sheet for Drosophila BioProject PRJDB5673_

.. csv-table::
    :file: ./_static/data/sample_sheet_adult.csv
    :widths: 10, 35, 45, 5, 5
    :header-rows: 1

Download the sample sheet file to your local computer: sample_sheet_adult.csv_

.. _sample_sheet_adult.csv: ./_static/data/sample_sheet_adult.csv
.. _PRJDB5673: https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJDB5673

Upload the sample sheet file to the GCP instance through the Jupyter server

.. image:: /_images/jupyter-2.png

.. image:: /_images/jupyter-3.png

Open a terminal to execute `pm4ngs-rnaseq`. This command will create an organizational data structure for the analysis.

.. image:: /_images/jupyter-4.png

In the terminal, activate the `pm4ngs_venv` virtual environment and execute the `pm4ngs-rnaseq` command.

The **pm4ngs-rnaseq** command line executed with the **--sample-sheet** option will let you type the different variables
required for creating and configuring the project. The default value for each variable is shown in the brackets. After
all questions are answered, the CWL workflow files will be
cloned from the github repo `ncbi/cwl-ngs-workflows-cbb`_ to the folder **bin/cwl**.

.. _ncbi/cwl-ngs-workflows-cbb: https://github.com/ncbi/cwl-ngs-workflows-cbb

.. code-block:: bash

    r78v10a07@instance-veraalva:~$ source pm4ngs_venv/bin/activate
    (pm4ngs_venv) r78v10a07@instance-veraalva:~$ ls
    pm4ngs_venv  sample_sheet_adult.csv
    (pm4ngs_venv) r78v10a07@instance-veraalva:~$ pm4ngs-rnaseq --sample-sheet sample_sheet_adult.csv

.. image:: /_images/jupyter-5.png

The project organizational data structure is:

.. code-block:: bash

    (pm4ngs_venv) r78v10a07@instance-veraalva:~$ tree -L 2 Dros_lol_mut/
    Dros_lol_mut/
    ├── LICENSE
    ├── README.md
    ├── bin
    │   └── cwl
    ├── config
    │   └── init.py
    ├── data
    │   └── PRJDB5673
    ├── doc
    ├── index.html
    ├── notebooks
    │   ├── 00 - Project Report.ipynb
    │   ├── 01 - Pre-processing QC.ipynb
    │   ├── 02 - Samples trimming.ipynb
    │   ├── 03 - Alignments and Quantification.ipynb
    │   ├── 04 - DGA.ipynb
    │   └── 05 - GO enrichment.ipynb
    ├── requirements
    │   └── conda-env-dependencies.yaml
    ├── results
    │   └── PRJDB5673
    ├── src
    └── tmp
    12 directories, 11 files