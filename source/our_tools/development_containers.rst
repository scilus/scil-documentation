Development containers
======================

To streamline the execution of the various technologies the lab develops on a wide range of computing architectures and operating systems, and to facilitate their distribution to collaborators, we use Docker images. An image is a stand-alone, executable package that includes everything needed to run a collection of softwares, including the code, runtimes, libraries, environment variables, and configuration files. In Docker, images are used to create containers, isolated and portable environments that can be run on any computer with Docker installed, regardless of the operating system running on the computer.

Two specialized images are developed for the lab and its collaborators:
* `Scilus <https://hub.docker.com/r/scilus/scilus/>`__: contains the :ref:`main dependencies <ref_scil_dependencies>`__ for the lab's projects, `Scilpy <https://github.com/scilus/scilpy>`__ and `dmriqcpy <https://github.com/scilus/dmriqcpy>`__
* `Scilus-flows <https://hub.docker.com/r/scilus/scilus-flows/>`__: contains :ref:`Nextflow <ref_nextflow>` and most pipelines developed by the lab, in addition to the content of Scilus.

.. _ref_dev_with_docker:

Developing with Docker
----------------------

To install Docker on your system, refer to the procedure :ref:`(here) <ref_docker_installation>`. Once Docker is installed, you can pull the Scilus image at a specific *<tag>* from the Docker Hub by running the following command:

.. code-block:: bash

    docker pull scilus/scilus:<tag>

To open a bash shell in container from the Scilus image, you can use the following command:

.. code-block:: bash

    docker run --rm -it scilus/scilus:<tag> /bin/bash

The ``--rm`` option will remove the container once you exit the shell. The ``-it`` options will open an interactive shell in the container, allowing you to launch commands. The ``/bin/bash`` command will open a bash shell in the container. You can then run any command available in the container, such as ``python``, ``git``, ``nextflow``, etc.

.. note::

    The ``--rm`` option is useful to avoid dangling containers on your system taking resources. However, if you want to keep the container, you can remove the ``--rm`` option. You can get the container ID using the ``docker ps`` command and attach to it using ``docker attach <ID>``. You can remove the container later with ``docker rm <ID>``.

Docker in Visual Studio code
----------------------------

`Visual Studio Code <https://code.visualstudio.com/>`__ is one of the IDE used by the lab. It is a free and open-source code editor developed by Microsoft. It includes support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring. It is also customizable, allowing users to change the theme, keyboard shortcuts, preferences, and install extensions that add additional functionality.

Visual Studio Code has a `Dev containers extension <https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers>`__ that allows you to develop inside a container. This is useful to avoid installing all the dependencies on your system and to ensure that the code will run in the same environment as the one used by the lab. To use this extension with the lab images, you need first to install Docker on your system and pull the Scilus image as described :ref:`above <ref_dev_with_docker>`.

Once done, open a folder in Visual Studio Code and click on the Docker icon in the left menu. This will open the Docker tab, listing containers, images available locally and in connected remote registries, and much more.

Click on the ``+`` icon in the *containers* pane and select ``Open current folder in container``. Choose a configuration from the list of base (Ubuntu is a good default one), the version of the base OS and additional features if desired, to generate a template configuration file. This will create a ``.devcontainer`` folder in your project with a ``devcontainer.json`` file. You can then edit this file to specify the image to use, the user to use in the container, the extensions to install, etc. To get an idea of a configuration for the lab, you can refer to the ``.devcontainer`` folder in the `Scilpy repository <https://github.com/scilus/scilpy>`__.

Once the configuration is done, click on the ``blue icon`` on the bottom left of the window and select ``Reopen in Container``. This will build the container and open a new window in the container.

You can then open a terminal in the container and run any command available in the container, such as ``python``, ``git``, ``nextflow``, etc. All files and directories in the project folder will be available in the container, allowing you to edit them in Visual Studio Code. You will also have access to all the dependencies installed in the container, pre-configured with the lab's settings.
