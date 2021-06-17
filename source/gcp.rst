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

