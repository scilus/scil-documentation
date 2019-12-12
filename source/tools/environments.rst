Developers
==============

.. role:: bash(code)
   :language: bash

Using environments
------------------

*Why?*

     What is an environment? Why should you use one?

     Most of the libraries we use and the programs we code are made in python. But also, most of the programs in Linux are based on python. We want to make sure that when we work, install libraries, uninstall libraries, etc., **we don’t break your Linux installation!** Environments are a good way to separate the system's python installation from the python version you need for your work.

     For instance, a python 3 environment will be necessary to use scilpy (the public repository) or Dipy1.0, but you might need a python 2 environment to work on our private repository of scilpy.

*What is it?*

    There are many options for environments. One very famous option is the Anaconda/conda world, but in the lab, we have experienced some issues with it. We highly recommand using `VirtualEnv <https://virtualenv.pypa.io/en/latest/>`_.

    .. code-block:: bash

        sudo pip install virtualenvwrapper
        mkdir ~/Envs
        NAME=somename # Ex: $NOM could be my_env_py3
                      # depending on the use you will give to this environment.
                      # Try to be explicit
        # One of:
        mkvirtualenv $NAME
        mkvirtualenv --python=python3.7 $NAME   # To use one precise python version
        mkvirtualenv $NAME --python=/usr/bin/python3.7  # Equivalent. The python
                                                        # version must be already
                                                        # installed on your computer

        # Note. To download a python version to your /usr/bin without installing it:
        # https://www.python.org/downloads/

| J'avais ça dans mes notes. Nécessaire?
| sudo apt install libblas-dev liblapack-dev gfortran cython python-dev
| sudo pip install setuptools

     Then you could add these lines in your .bashrc:

    - From a terminal: :bash:`sudo gedit ~/.bashrc`
    - Copy this in your file:

        .. code-block:: bash

            export WORKON_HOME=~/Envs/
            source /usr/local/bin/virtualenvwrapper.sh

*How to install it?*

    When everything is set, restart your terminal. You should now be able to work in a chosen environmnent by using :bash:`workon $NAME`. Now everytime you need to install a new library inside the environment, you should always try to use :bash:`pip install your_library`. The environment will use the right pip based on the current python version. *Don't use sudo pip!* It will use the pip of the system!

    If the library can't be installed via pip, however, you can use :bash:`sudo apt-get install your_library`. In this case the `sudo` will not be a problem.