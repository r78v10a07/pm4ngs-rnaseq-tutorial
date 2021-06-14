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

.. image:: /_images/jupyter-6.png

Pre-processing QC
-----------------

The first notebook download the SRA data using the accessions defined in the sample sheet. Execute all cells until the
**Retrieving data using fastq-dump**. This cell will submit the CWL workflow. Open a terminal to check that the
**fastq-dump** command is working.

.. image:: /_images/jupyter-7.png

Once all cells are execute completely the *fastq* samples will be available at the **data/PRJDB5673** directory. Run
the **tree** command to visualize the data structure.

.. code-block:: bash

    (pm4ngs_venv) r78v10a07@instance-veraalva:~$ tree -L 3 Dros_lol_mut/

.. image:: /_images/jupyter-8.png

The pre-processing table is available in the `00 - Project Report` notebook. The links in the table gives access to the
FastQC_ reports for each sample. The reports are used to select the trimming parameters.

.. image:: /_images/jupyter-9.png

.. image:: /_images/jupyter-10.png

.. image:: /_images/jupyter-11.png

.. image:: /_images/jupyter-12.png

.. _FastQC: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/

Samples trimming
----------------

Trimmomatic_ performs a variety of useful trimming tasks for illumina paired-end and single ended data.The selection
of trimming steps and their associated parameters are supplied on the command line.

The current trimming steps are:

 * ILLUMINACLIP: Cut adapter and other illumina-specific sequences from the read.
 * SLIDINGWINDOW: Perform a sliding window trimming, cutting once the average quality within the window falls below a threshold.
 * LEADING: Cut bases off the start of a read, if below a threshold quality
 * TRAILING: Cut bases off the end of a read, if below a threshold quality
 * CROP: Cut the read to a specified length
 * HEADCROP: Cut the specified number of bases from the start of the read
 * MINLEN: Drop the read if it is below a specified length
 * TOPHRED33: Convert quality scores to Phred-33
 * TOPHRED64: Convert quality scores to Phred-64

It works with FASTQ (using phred + 33 or phred + 64 quality scores, depending on the Illumina pipeline used), either
uncompressed or gzipp'ed FASTQ. Use of gzip format is determined based on the .gz extension.

PM4NGS uses standard options for Trimmomatic but in this example we need to add **HEADCROP:10** as it is shown in next
figure:

.. image:: /_images/jupyter-13.png

Updating the `00 - Project Report` notebook.

.. image:: /_images/jupyter-14.png

Check the FastQC reports to check if the trimming reduced the distortion in the first 10 bases.

.. image:: /_images/jupyter-15.png

.. _Trimmomatic: http://www.usadellab.org/cms/?page=trimmomatic

Alignment and Quantification
----------------------------

