Intro to Containers
===================

.. role:: bash(code)
   :language: bash


Container technologies are used by computer scientists and engineers in research and industry. They allow applications and services to be packaged into isolated, self-contained units that can be deployed on any cloud or local host. This provides a great deal of flexibility and portability for computing tasks. 

By using containers, computer scientists can avoid the time-consuming task of setting up and configuring computing environments, since the containerized applications can run on any platform without modifications. This is especially useful when attempting to replicate research results or share data between teams. Furthermore, the use of containers also helps to ensure that all software dependencies are met, making code more reliable and reproducible.

In addition, containers can be used to improve security by isolating applications from each other and the host operating system. This can help prevent malicious software from accessing sensitive data or causing system crashes. Finally, using containers can help reduce hardware costs by allowing multiple applications to run on the same physical hardware.

**TLDR:** They are like tiny isolated computers running on other computers. They keep things separated when dealing with multiple tools that you do not want to install over and over again or to avoid unwanted interactions.

Singularity
-----------
Singularity containers are designed to be more secure and flexible for high-performance computing and scientific computing workloads. One key difference is that Singularity containers can run without elevated privileges or root access, making them more suitable for multi-user and shared environments

Since they contain the Operating System (OS), all dependencies, libraries and software, data, etc., they can be large files (Gigabytes). Once a Singularity is created, it is fixed in time. You cannot modify what is inside, re-install a toolbox or add new files. This means that you need to know where you got it from, when you downloaded it and make sure to keep an meaningful filename to know which containers you have. 

:bash:`singularity exec` to run a command inside a container. This allow you to run a single (or a few) command as if you had everything installed, it allows you to launch command anywhere without having to install everything first. It is useful when a software is hard (or impossible) to install on a cluster or a specific OS, but you need that software for processing.

:bash:`singularity shell` to open a shell inside the container for interactive use. If you do not know exactly what command to run, you can spawn a terminal and try a few command, run something and explore. This act as a normal bash terminal as if you had everything install.

:bash:`singularity build` to create a new container from a recipe file. If you have a recipe file defining how to install everything (LINK). You can create your Singularity from it, it is useful when doing small modifications to the original Singularity. It is also easier to share this recipe on Github or with collaborators than sharing a 10GB Singularity file.

Installations
^^^^^^^^^^^^^
Functional MRI
""""""""""""""

Docker
------

Windows Subsystem for Linux
----------------------------

asd

:bash:`feat` is a user-friendly FMRI analysis tool that includes data preprocessing, timeseries analysis, and group analysis using Bayesian techniques.

.. code-block:: bash

    # export FSLDIR=/PATH/TO/FSL
    . ${FSLDIR}/etc/fslconf/fsl.sh
    export PATH=${FSLDIR}/bin:${PATH}

ANTs (Advanced Normalization Tools) is a powerful open-source software package for (medical) image analysis registration and segmentation. Extremely useful to create templates or extract cortical thickness. It is widely used in the field of neuroimaging.
You can find information on their `Github page <https://github.com/ANTsX/ANTs>`__ or on their new `documentation <http://stnava.github.io/ANTsDoc/>`__.


.. figure:: /images/intro_to_software_fsl.png
    :scale: 40 %
    :align: center

    FSLeyes is used here to visualize fMRI data.