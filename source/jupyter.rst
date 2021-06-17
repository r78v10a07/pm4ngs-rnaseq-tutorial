.. _jupyter:

The Jupyter Server
==================

Jupyter is a free, open-source, interactive web tool known as a computational notebook, which researchers can use
to combine software code, computational output, explanatory text and multimedia resources in a single document.
Computational notebooks are essentially laboratory notebooks for scientific computing that keep track of all steps
in a research project. Jupyter notebooks can be shared with collaborators and are used to guarantee reproducibility.

The Jupyter notebook has two components. Users input programming code or text in rectangular cells in a front-end web
page. The browser then passes that code to a back-end ‘kernel’, which runs the code and returns the results. The kernel
reside in the server, executing all code in that computer and the front-end in the user local browser.

Read this interesting article about Jupyter Notebooks for data scientists: https://www.nature.com/articles/d41586-018-07196-1

Accessing the instance with SSH
-------------------------------

Click on the **SSH** button to login.

.. image:: /_images/instances.png
    :alt: Instances

After clicking the **SSH** button, a new windows will be open. This is a Linux terminal running directly in the instance.

.. image:: /_images/terminal-1.png
    :alt: Linux terminal

Activating pm4ngs_venv virtual environment
------------------------------------------

Everytime we login into the instance, we need to activate the **pm4ngs_venv** virtual environment. This mean that we
will be using the python packages installed in this virtual environment instead of the packages in the instance.

.. code-block:: bash

    veraalva@instance-veraalva:~$ source pm4ngs_venv/bin/activate

Running the Jupyter Server
--------------------------

Open a terminal and activate the **pm4ngs_venv** virtual environment and run the jupyter server. As the GCP instance
is a remote computer, we need to run the jupyter server with the **--port** and **--ip** options.

Creates a password for the Jupyter server:

.. code-block:: bash

    (pm4ngs_venv) r78v10a07@instance-veraalva:~$ jupyter notebook password

Start the Jupyter server

.. code-block:: bash

    (pm4ngs_venv) r78v10a07@instance-veraalva:~$ jupyter notebook --no-browser --port=8888 --ip=0.0.0.0

.. image:: /_images/terminal-4.png
    :width: 600px
    :alt: Start the jupyter notebook server

Open the jupyter web interface in your local computer
-----------------------------------------------------

Get the **External IP** for your instance in the GCp Cloud console: **VM instances**. Then, type the address in your
local browser plus the jupyter server port: **:8888**

.. image:: /_images/jupyter-1.png
    :width: 600px
    :alt: Jupyter web interface
