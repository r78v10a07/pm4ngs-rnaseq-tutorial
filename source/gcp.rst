.. _gcp:

GCP Instance Setup
==================

Create a GCP instance
---------------------

Create a GCP instance with 16 CPUs and 60GB of RAM (machine type: **n1-standard-16**). Click on **Change** button in the
**Boot disk** box to select Operating system: Ubuntu, Version: Ubuntu 20.04 LTS. Click on **Management** to select
**Preemptibility: ON**

.. image:: /_images/instance-creation.jpg
    :alt: GCP instance creation

Accessing the instance with SSH
-------------------------------

The instance will be available with two IP address, one internal for GCP and another external accessible from Internet.
Click on the **SSH** button to login.

.. image:: /_images/instances.png
    :alt: Instances

After clicking the **SSH** button, a new windows will be open. This is a Linux terminal running directly in the instance.

.. image:: /_images/terminal-1.png
    :alt: Linux terminal

Installing dependencies on the GCP instance with Ubuntu
-------------------------------------------------------

Runs these commands on a terminal to prepare the instance to run PM4NGS

.. code-block:: bash

    veraalva@instance-veraalva:~$ sudo apt-get update
    veraalva@instance-veraalva:~$ sudo apt-get install docker.io python3 python3-pip python3-venv python3-dev poppler-utils gcc nodejs tree
    veraalva@instance-veraalva:~$ sudo usermod -aG docker $USER
    veraalva@instance-veraalva:~$ logout

Close and reopen the terminal to set the docker group in the user. Then, click on the SSH button again to re-launch the
terminal.

Testing the Docker daemon
-------------------------

.. code-block:: bash

    veraalva@instance-veraalva:~$ docker run hello-world

Docker will pull the **hello-world** image and run it in a container. A **Hello from Docker!** message is displayed in
the terminal.

.. image:: /_images/terminal-2.png
    :alt: Testing Docker

Installing PM4NGS
-----------------

Creates a Python virtual environment named: **pm4ngs_venv** for installing PM4NGS

.. code-block:: bash

    veraalva@instance-veraalva:~$ python3 -m venv pm4ngs_venv
    veraalva@instance-veraalva:~$ source pm4ngs_venv/bin/activate
    (pm4ngs_venv) veraalva@instance-1:~$ pip install wheel
    (pm4ngs_venv) veraalva@instance-1:~$ pip install pm4ngs

Testing PM4NGS
--------------

Test PM4NGS RNA-Seq module:

.. code-block:: bash

    (pm4ngs_venv) veraalva@instance-veraalva:~$ pm4ngs-rnaseq

.. image:: /_images/terminal-3.png
    :alt: Testing PM4NGS

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


