.. _python:

Installing PM4NGS
=================

Read PM4NGS published manuscript in GIGAScience_

.. _GIGAScience: https://academic.oup.com/gigascience/article/10/1/giaa141/6067195


What is a Python virtual environment?
-------------------------------------

A python virtual environment is a "new Python installation" with their own site directories, optionally isolated from
system site directories. Each virtual environment has its own Python binary (which matches the version of the binary
that was used to create this environment) and can have its own independent set of installed Python packages in its
site directories.

Creation of virtual environments is done by executing the command venv:

.. note::

    python3 -m venv /path/to/new/virtual/environment

Running this command creates the target directory (creating any parent directories that don’t exist already), a common
name for the target directory uses as suffix  *_venv*. It also creates a bin subdirectory containing a copy/symlink of the Python
binary/binaries. It also creates an (initially empty) *lib/pythonX.Y/site-packages* subdirectory for the new packages.
If an existing directory is specified, it will be re-used.

Once a virtual environment has been created, it can be **“activated”** using a script in the virtual environment’s
binary directory. The invocation of the script is platform-specific (<_venv> must be replaced by the path of the
directory containing the virtual environment):

.. note::

    $ source /path/to/new/virtual/environment/bin/activate

Installing PM4NGS
-----------------

Creates a Python virtual environment named: **pm4ngs_venv** for installing PM4NGS.

.. code-block:: bash

    veraalva@instance-veraalva:~$ which python3
    /usr/bin/python3
    veraalva@instance-veraalva:~$ python3 -m venv pm4ngs_venv
    veraalva@instance-veraalva:~$ source pm4ngs_venv/bin/activate
    (pm4ngs_venv) veraalva@instance-veraalva:~$ which python3
    /home/r78v10a07/pm4ngs_venv/bin/python3
    (pm4ngs_venv) veraalva@instance-1:~$ pip install wheel
    (pm4ngs_venv) veraalva@instance-1:~$ pip install pm4ngs

These commands need to be executed only one time during the tutorial.

Testing PM4NGS
--------------

Test PM4NGS RNA-Seq module:

.. code-block:: bash

    (pm4ngs_venv) veraalva@instance-veraalva:~$ pm4ngs-rnaseq

.. image:: /_images/terminal-3.png
    :alt: Testing PM4NGS

