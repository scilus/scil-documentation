.. _ref_ants:

ANTs
====

.. role:: bash(code)
   :language: bash

*What is it?*

    ANTs is a normalization tools. You can find information on their `Github page <https://github.com/ANTsX/ANTs>`_ or on their new `documentation <http://stnava.github.io/ANTsDoc/>`_.

    We use it for the following purposes:

    1. To compute nonlinear SyN registration or simple linear registration. The wrapper script antsRegistrationSyN.sh is used extensively. The main use is to bring any subject to MNI space or to bring the T1 weighted image into the diffusion space. A unique feature of this algorithm is its ability to be run in multivariate fashion, i.e. be able to have a series of moving and fixed images that the optimization algorithm uses to find best alignment.  As the moment, ANTS is the cutting-edge registration tool in the community, i.e. superior to FSL, SPM, ...
    2. To build templates. Suppose you want to build a FA or T1 template of your aging brain population (or any population). We use ANTS for this.
    3. To perform skull-stripping or brain extraction. This is done with registration and a template. It usually takes 20-30 minutes but can be more robust than FSL bet.
    4. To segment WM-GM-CSF and to compute cortical thickness. This is a less common usage in the lab.

*How to install it?*

    You can find instructions on `ANTs github page <https://github.com/ANTsX/ANTs/wiki/Compiling-ANTs-on-Linux-and-Mac-OS>`_, but from our tests it seems easier to use `Neurodebian's page <http://neuro.debian.net/pkgs/ants.html>`_ (click on "Install this package", select your system, choose any download server and follow instructions*). To check your installation, start typing 'ant' in your terminal and hit tab twice. You should see a list of ants options such as 'antsRegistrationSyNQuick.sh'.

    Then add this line to your bashrc:  `export ANTSPATH=/usr/lib/ants/`

    \* Be careful though as these instructions can create errors in your sources.list. If you see warnings when running apt-get update, you probably now have twice the same key. Use your favorite editor to delete the doublons.
