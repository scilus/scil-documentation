.. _ref_setupcomputer:

.. role:: bash(code)
   :language: bash

Setting up your computer
========================

Before you can start working with the tools commonly-used or developped in the lab, you need to setup your computer. Follow this step-by-step guide to get your computer ready to work.

*This section is a work in progress. Eventually, it should cover OS choices, IDE choice, python and virtualenv installation, scilpy installation, nextflow and singularity/docker.*

We recommend using Linux, but Mac and Windows can also be viable. If you already have a computer with Linux (or Mac) installed, proceed to the next step. If you want to install Linux on your personal computer but also want to keep Windows, you have two choices:

    1) You can dual-boot Linux and Windows by following one of the many tutorials online, such as this `one <https://www.freecodecamp.org/news/how-to-dual-boot-windows-10-and-ubuntu-linux-dual-booting-tutorial/>`_. This process can be tedious so don't hesitate to ask for help in the lab.

    2) You can use WSL2 on Windows 10 or 11. A step-by-step guide is available here (*TODO add link to new section*) to help you install WSL2.

IDE
"""

An integrated development environment (IDE) is an application made for software development, including code editing, debugging, and testing. Most people at the lab use `VSCode <https://code.visualstudio.com/download>`_, which is always free and compatible on all platforms. Installing this first will be helpful for some of the next steps.

Terminal and bash
"""""""""""""""""

Now is the time to open a bash terminal, also known as the command line. The terminal allows you to execute commands, manage files and folders, and automate tasks. You will use it to install all you need to complete the setup of your computer.

It is useful to learn some of the basics of the bash language to help you play around. Please refer to this cheat sheet on the bash language (*TODO add link to new section*).

Before proceeding to the next steps, here are some useful additions you can make to your terminal "settings", by modifying what we call the *.bashrc*. First, open the .bashrc in VSCode by typing in the terminal :bash:`code .bashrc` (make sure you are in your home directory by simply typing :bash:`cd`). Then, choose the features you like!

* | If you want your terminal to display helpful colors and show your current git branch:

.. code-block:: bash

    # Replace this part:

    if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
    else
        PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
    fi
    unset color_prompt force_color_prompt

    # by this part:

    ########### Custom prompt for GIT ###############
    parse_git_branch () {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
    }

    parse_git_tag () {
     git describe --tags 2> /dev/null
    }

    parse_git_branch_or_tag() {
     local OUT="$(parse_git_branch)"
     if [ "$OUT" == " ((no branch))" ]; then
       OUT="($(parse_git_tag))";
     fi
     echo $OUT
    }
    #################################################

    if [ "$color_prompt" = yes ]; then
        # Using Git branch parsing
        PS1="${debian_chroot:+($debian_chroot)}\[\e[34;1m\]\u@\[\e[33;1m\]\h:\[\033[01;34m\]\w\[\e[32;1m\]\$(parse_git_branch_or_tag)\[\e[31;1m\]\[\033[00m\]\[\e[31;1m\]$\[\e[0m\] "
    else
        # Using Git branch parsing
        PS1="${debian_chroot:+($debian_chroot)}\u@\h:\w\$(parse_git_branch_or_tag)\$ "
    fi
    unset color_prompt force_color_prompt

* | If you want some useful aliases and keybinds, copy this at the end of your .bashrc:

.. code-block:: bash

    # Useful aliases
    alias c='clear'
    alias histg='history | grep'

    # History auto-complete navigation
    bind '"\e[5~": history-search-backward'
    bind '"\e[6~": history-search-forward'

Python
""""""

Although your Linux distribution most likely already includes a python distribution, it may be necessary to install additionnal python packages for software development. There are many alternatives for installing python. On Ubuntu, we can use the `deadsnakes <https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa>`_ repository to download and install a specific version:

.. code-block:: bash

        sudo add-apt-repository ppa:deadsnakes/ppa
        sudo apt-get install python3.10-dev python3.10-venv python3.10-tk python3-pip
        python3.10 -m pip install pip  # update pip (python package manager) to latest version

Other python packages can be installed by replacing python3.X by a version of your choice.

Virtual environments
""""""""""""""""""""

Virtual environments are a good way to separate the system's python installation from the python version you need for your work. It also allows you to have a precise set of python packages with specific versions. While there are many options for environments, we highly recommand using `VirtualEnv <https://virtualenv.pypa.io/en/latest/>`_. Start by installing it and creating a directory where all your environments will be saved:

.. code-block:: bash

    sudo pip install virtualenvwrapper
    mkdir ~/Envs

Then you should add these lines in your .bashrc:

.. code-block:: bash

    export WORKON_HOME=~/Envs/
    #export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3   # uncomment this line if you have errors when starting your terminal (next step)
    source /usr/local/bin/virtualenvwrapper.sh

Finally, you can restart the terminal and create an environment:

.. code-block:: bash

    NAME=somename # Ex: $NAME could be my_env_py3
                    # depending on the use you will give to this environment.
                    # Try to be explicit
    # One of:
    mkvirtualenv $NAME
    mkvirtualenv --python=python3.10 $NAME   # To use one precise python version
                                                # You can also use the complete path to the python installation
    mkvirtualenv $NAME --python=/usr/bin/python3.10  # Equivalent. The python
                                                        # version must be already
                                                        # installed on your computer

    # Note. To download a python version to your /usr/bin without installing it:
    # https://www.python.org/downloads/

When everything is set, restart your terminal. You should now be able to work in a chosen environmnent by using :bash:`workon $NAME`. Now everytime you need to install a new library inside the environment, you should always try to use :bash:`pip install your_library`. The environment will use the right pip based on the current python version. *Don't use sudo pip!* It will use the pip of the system!

If the library can't be installed via pip, however, you can use :bash:`sudo apt-get install your_library`. In this case the `sudo` will not be a problem.

You might want to always have a specific environment when opening a terminal. To do so, simply open the .bashrc and copy-paste this :bash:`workon somename` at the end of it (don't forget to replace :bash:`somename` by the actual name of your environment!).

Git
"""

Scilpy
""""""

Containers
""""""""""

Nextflow
""""""""

Super computers
"""""""""""""""

The first use of a computing platform can be tricky but you'll get used to it. Please see the (:ref:`ref_heavy_computing`) tab for more information and for our first-use tutorial. If your goal is to use the computing platform to run Tractoflow, you will find instructions on the :ref:`ref_tractoflow` page. Else see the :ref:`ref_other_pipelines` page.

SSH and VPN
"""""""""""

    If you work from home, you might need to connect to the UdeS network for the follow reasons.

    * | To have access to scientific papers (ex, free access to many articles in Google scholar): See the VPN information below or go on the University's `library's website <https://www.usherbrooke.ca/biblio/trouver-des/articles-de-periodiques-revues-et-journaux/>`_ and click on "Outil de découverte" if your are logged in with your CIP (top-right corner, the connexion button).

    * | To connect to your lab computer: Use ssh (see below).

VPN
    Follow `these instructions <https://www.usherbrooke.ca/services-informatiques/repertoire/reseaux/rpv/>`_ to connect through **VPN**.

    **(we might want to write a summary for English speakers)**

SSH
    1. Connect to the University's VPN.

    2. You must know your lab computer's IP address or its University code (ex: DINF-0000-00a), which should be written on the computer. (Ask a research assistant if you don't know).

    3. | Connect with ssh. On Linux, Mac or WSL (Windows), ssh can be simply used via the terminal. The option -X is to make sure the applications you use appear at home.
       | ``ssh -x your_cip@your_computer_IPaddress``, or
       | ``ssh -X your_cip@DINF-0000-00a.dinf.fsci.usherbrooke.ca``.

       It can be useful to create an alias for this in your personal computer's .bashrc. Simply open the .bashrc and copy-paste this at the end of it (you can change the name ScilTour for whatever you want):

       :bash:`alias ScilTour='ssh -X your_cip@DINF-0000-00a.dinf.fsci.usherbrooke.ca -o ServerAliveInterval=10'`

    On Windows, you can also use MobaXterm. Download it, then click on Session, SSH. In Remote host, enter your IP address. In Advanced SSH settings, make sure the X11-Forwarding button is clicked.

Other tools
"""""""""""
