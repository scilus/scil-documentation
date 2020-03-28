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
    4. To ssegment WM-GM-CSF and to compute cortical thickness. This is a less common usage in the lab.

*How to install it?*

    These instructions are base on `ANTs instructions here <https://github.com/ANTsX/ANTs/wiki/Compiling-ANTs-on-Linux-and-Mac-OS>`_. Alternatively, you can try 'apt-get install ants':

    .. code-block:: bash

        cd my_favorite_dir
        mkdir ANTs
        cd ANTs
        git clone https://github.com/ANTsX/ANTs.git code
        workingDir=${PWD}
        mkdir build install
        cd build
        cmake -DCMAKE_INSTALL_PREFIX=${workingDir}/install \
            ${workingDir}/code 2>&1 | tee cmake.log
        make -j 4 2>&1 | tee build.log
        cd ANTS-build
        make install 2>&1 | tee install.log

    Then add these lines in your .bashrc:

    - From a terminal: :bash:`gedit ~/.bashrc`
    - Copy this in your file:

        .. code-block:: bash

            export ANTSPATH=/opt/ANTs/bin/
            export PATH=${ANTSPATH}:$PATH