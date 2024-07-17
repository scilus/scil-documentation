.. _ref_setupcomputer:

.. role:: bash(code)
   :language: bash

Setting up your computer
========================

Before you can start working with the tools commonly-used or developped in the lab, you need to setup your computer. Follow this step-by-step guide to get your computer ready to work. 

*If you work on a personal computer, you might be interested in visiting* :ref:`ref_setuppersocomputer` *first!*

IDE
"""

An integrated development environment (IDE) is an application made for software development, including code editing, debugging, and testing. Most people at the lab use `VSCode <https://code.visualstudio.com/download>`_, which is always free and compatible on all platforms. Installing this first will be helpful for some of the next steps.

Terminal and bash
"""""""""""""""""

Now is the time to open a bash terminal, also known as the command line. The terminal allows you to execute commands, manage files and folders, and automate tasks. You will use it to install all you need to complete the setup of your computer.

It is useful to learn some of the basics of the bash language to help you play around. Please refer to this cheat sheet on the bash language (*TODO add link to new section*).

Before proceeding to the next steps, here are some useful additions you can make to your terminal "settings", by modifying what we call the *.bashrc*. First, open the .bashrc in VSCode by typing in the terminal :bash:`code ~/.bashrc`, then, copy-paste these lines at the end of it:

.. code-block:: bash

    # Useful aliases
    alias c='clear'
    alias histg='history | grep'

    # History auto-complete navigation
    bind '"\e[5~": history-search-backward' # Press page-up button to go backward in history
    bind '"\e[6~": history-search-forward' # Press page-down button to go forward in history

Python
""""""

Although your Linux distribution most likely already includes a python distribution, it may be necessary to install additionnal python packages for software development. There are many alternatives for installing python. On Ubuntu, we can use the `deadsnakes <https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa>`_ repository to download and install a specific version:

.. code-block:: bash

        sudo apt-get update
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

Then you should add these lines in your .bashrc (:bash:`code ~/.bashrc`):

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

When everything is set, restart your terminal. You should now be able to work in a chosen environment by using :bash:`workon $NAME`. Now everytime you need to install a new library inside the environment, you should always try to use :bash:`pip install your_library`. The environment will use the right pip based on the current python version. *Don't use sudo pip!* It will use the pip of the system!

You might want to always have a specific environment when opening a terminal. To do so, simply open the .bashrc and copy-paste this :bash:`workon somename` at the end of it (don't forget to replace :bash:`somename` by the actual name of your environment).

Git
"""

Git is a version control software system that allows to store and keep track of the changes made to a code base. It is a kind of a "dropbox" for code, which saves the whole evolution (versions) of the code. In the lab, we use the website `Github <https://github.com/>`_ to help us store and manage our code using Git in a user-friendly way. You should get used to it from the beginning, as it is a powerful and very helpful tool. If you have never used Git on your computer, the first step would be to set your user.name and user.email:

.. code-block:: bash

    git config --global user.name "FIRST_NAME LAST_NAME"
    git config --global user.email "MY_NAME@example.com"

You can also add these lines in your .bashrc (:bash:`code ~/.bashrc`) to see the current Git branch in your terminal:

.. code-block:: bash

    # Custom prompt for Git 
    git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/[\1] /'
    }
    PS1="\$(git_branch)$PS1"

In the next steps, you will have to *clone* and *fork* Git repositories. In short, *cloning* a repository means "downloading" it to your computer using the :bash:`git clone` command with the link found by clicking on the green "<> Code" button on the Github page of the repository, under the SSH tab. Moreover, *forking* a repository means creating your own version of the repository by clicking on the "Fork" button on the Github page of the repository.

To connect to Github without supplying your username and password each time you interact with Git, it is useful to add a SSH key to your Github account. This `link <https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=linux>`_ explains in details the procedure. For the next steps, we assume that your SSH key is set and working. If it is not the case, you can always use the URL in the HTTPS tab of the green "<> Code" button when cloning a repository.

See the :ref:`ref_git` page for more details of its usage.

Scilpy
""""""

`Scilpy <https://github.com/scilus/scilpy>`_ is the main library supporting research and development at the lab. It currently supports python versions 3.8 to 3.10, so make sure you have followed all the previous steps. Once your python distribution is correctly installed and your virtual environment is active, scilpy can be installed by following the procedure outlined below:

    .. code-block:: bash

        # If you never installed libfreetype6-dev
        sudo apt install libfreetype6-dev

        # If you intend to use COMMIT/AMICO (on LINUX or WSL)
        sudo apt install libblas-dev liblapack-dev

        # If you intend to use COMMIT/AMICO (on MAC)
        brew install openblas lapack

        # Make a fork of scilpy to be able to modify your own version of the code.
        # Go where you want the scilpy folder to be, then:
        git clone git@github.com:YOUR_USERNAME/scilpy.git # Don't forget to replace YOUR_USERNAME
        cd scilpy 
        pip install -e .

        # Setup your Git remotes
        git remote add upstream git@github.com:scilus/scilpy.git # Link to the main version of scilpy
        git remote add origin git@github.com:YOUR_USERNAME/scilpy.git # Should be set automatically
        git remote -v # To verify everything is in order

| *Note: Scilpy can now be installed in a virtual environment through pip:* :bash:`pip install scilpy`.
| *Note: For Mac users, you might have to use this command instead* :bash:`pip install scilpy==2.0.0 --use-pep517`.


In any case, please refer to the `Github page <https://github.com/scilus/scilpy>`__ if you encounter problems.

.. _ref_containers:

Containers
""""""""""

Container technologies allow applications and services to be packaged into isolated, self-contained units that can be deployed on any cloud or local host. They are like tiny isolated computers running on other computers. For more information, visit the guide on containers and virtual machines (:ref:`ref_virtualmachines`). A container bundling all the dependencies required for running any flow (see section :ref:`ref_flow`) developped in the lab is available `here <https://hub.docker.com/r/scilus/scilus>`__. In the lab, we use Docker and Apptainer (formerly Singularity) containers, which we describe below.

Docker
------
The most popular container technology is undoubtedly Docker. Docker is supported on Mac, Windows and Linux, although it'd seem like Docker running a Linux instance do not work well on MacOS with M1/M2 CPU. To install Docker, follow this documentation: `<https://docs.docker.com/engine/install/ubuntu>`__.

However, make sure you follow these subsections:
    - Uninstall old versions (sometimes `this <https://askubuntu.com/questions/935569/how-to-completely-uninstall-docker>`__ is necessary, answer #1)
    - Install using the apt repository 
    - Set up the repository
    - Install Docker Engine

Once installed, you will have to add yourself to the group of users that can run Docker with *sudo* privileges and restart Docker.

.. code-block:: bash

    sudo groupadd docker
    sudo gpasswd -a ${USER} docker
    sudo service docker restart

Launch :bash:`docker --version` to verify if it is installed correctly.

Apptainer
---------

Apptainer (formerly Singularity) is an alternative to Docker. Docker requires root privileges and, as such, is not available on High Performance Computers from the Digital Alliance of Canada (see section :ref:`ref_highperfcomputer`). However, Apptainer containers can run without elevated privileges or root access. Apptainer is particularly useful for saving a Docker container to a file which is then useable in High performance computers, without root privileges.

The steps for installing Apptainer on Ubuntu are given below. **Do not try to install on MacOS!** To use on Digital Alliance of Canada clusters, refer instead to section: :ref:`ref_highperfcomputer`.

.. code-block:: bash

    sudo apt update
    sudo apt install -y software-properties-common
    sudo add-apt-repository -y ppa:apptainer/ppa
    sudo apt update
    sudo apt install -y apptainer

Additional information can be found on the official documentation: `<https://apptainer.org/docs/admin/main/installation.html#install-ubuntu-packages>`__.

Finally, launch :bash:`apptainer --version` to verify if it is installed correctly.


Nextflow
""""""""

Nextflow is an open-source pipelining tool that makes processing massive datasets and building workflows somewhat easy. We use it in the lab to run our various :ref:`ref_flow`.

Nextflow can be used on Linux, MacOS and WSL (Windows). It requires Bash 3.2 (or later) and Java 11 (or later, up to 20) to be installed. To find your Java version, use :bash:`java -version`. If it is not satisfying the requirement, follow these steps in a terminal:

.. code-block:: bash

    # Install SDKMAN
    curl -s https://get.sdkman.io | bash

    # Open a new terminal
    sdk install java 17.0.10-tem
    
    # Confirm that everything is alright
    java -version


It is common to explicitely tell Nextflow where Java is. Use this command: :bash:`readlink -f \`which javac\` | sed "s:/bin/javac::"` to get the full path. Then, add this line to your .bashrc: :bash:`export JAVA_HOME=/PATH/FOR/JAVA/YOU/JUST/GOT`

Now you can install Nextflow by opening a terminal and executing the following lines in a directory of your choice (likely next to the rest of your tools):

.. code-block:: bash

    # Don't forget to be in your chosen directory
    curl -s https://get.nextflow.io | bash
    chmod +x nextflow

    # Confirm that Nextflow is installed correctly
    nextflow info

    # Change the Nextflow version to v21.12.1 (required for our flows)
    echo 'export NXF_VER=21.12.1-edge' >> ~/.bashrc

    # To execute Nextflow from anywhere, we add the current directory to PATH in your .bashrc
    echo 'export PATH=$PATH:'$(pwd) >> ~/.bashrc

    # Apply the changes to .bashrc
    source ~./bashrc

    # Test Nextflow
    ./nextflow run hello

.. _ref_highperfcomputer:

High performance computers
""""""""""""""""""""""""""

The first use of a computing platform can be tricky but you'll get used to it. Here we explain how to get started on Beluga, one of the high performance computers (HPC) of the Digital Research Alliance of Canada (formerly Compute Canada). 

Connect to Beluga via ssh with :bash:`ssh USER@beluga.computecanada.ca`.

On your first visit, you will probably want to edit your .bashrc with your preferences. Since VSCode will not be available, you will have to use an editor built in the terminal like Nano (:bash:`nano ~/.bashrc`) or Vim (:bash:`vim ~/.bashrc`). Please refer to the :ref:`ref_linux` if you don't know these tools.

Everytime you log in Beluga, you will need to load the modules necessary for your needs (scilpy, tractoflow, etc). Here are the modules currently needed for running Nextflow pipelines:

.. code-block:: bash

    module load StdEnv/2020
    module load nextflow/21.10.3
    module load apptainer/1.1.8

However, if you want to install scilpy, open a new session and follow these steps:

.. code-block:: bash

    module load StdEnv/2023 python/3.10 vtk
    virtualenv --no-download --clear ~/Envs/scilpy && source ~/Envs/scilpy/bin/activate
    pip install --no-index --upgrade pip
    pip install pygit2~=1.12.0 scilpy==2.0.2
    python -c 'import scilpy'

In the future, you will need to follow these steps to work with scilpy after opening a new session:

.. code-block:: bash

    module load StdEnv/2023 python/3.10 vtk
    source ~/Envs/scilpy/bin/activate

Note that it is currently not possible to work with both scilpy and Nextflow on the same session, as they require different module versions. If you need both these packages at the same time, you might want to consider using :ref:`ref_containers`.

Please see the (:ref:`ref_heavy_computing`) tab for more information about the usage of such resources. If your goal is to use the computing platform to run Tractoflow, you will find instructions on the :ref:`ref_tractoflow` page.
