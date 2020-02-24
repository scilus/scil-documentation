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

    In a terminal, from the directory where you want to install it:

    .. code-block:: bash

        mkdir ANTs
        cd ANTs
        git clone https://github.com/stnava/ANTs.git code
        mkdir build
        cd build
        ccmake ../code # Press c twice and then g
        make -j 8      # -j is the number of threads.
                       # If your computer doesn't allow 8, simply decrease this number.
        cp ../code/Scripts/*.sh bin/

    Then add these lines in your .bashrc:

    - From a terminal: :bash:`gedit ~/.bashrc`
    - Copy this in your file:

        .. code-block:: bash

            export PATH=~/code/ANTs/build/bin:${PATH}
            export ANTSPATH=~/code/ANTs/build/bin