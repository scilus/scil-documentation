.. _ref_python_dist:


Python distributions
====================

.. role:: bash(code)
   :language: bash

Although your Linux distribution most likely already includes a python distribution, it may be necessary to install additionnal python packages for software development. There are many alternatives for installing python. On Ubuntu, we can use the `deadsnakes <https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa>`_ repository to download and install a specific version:

.. code-block:: bash

        sudo add-apt-repository ppa:deadsnakes/ppa
        sudo apt-get install python3.7-dev python3.7-venv python3.7-tk python3-pip  # python3.7 works well for scilpy
        python3.7 -m pip install pip  # update pip (python package manager) to latest version

Other python packages can be installed by replacing python3.X by a version of your choice.
