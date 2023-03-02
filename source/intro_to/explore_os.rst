Intro to Linux
=======================

.. role:: bash(code)
   :language: bash

Exploring the OS
"""""""""""""""""""""""
Linux is a free and open-source operating system that is available in many different flavors or distributions. Unlike Windows or MacOS, Linux is not controlled or owned by a single company and is instead developed by a global team of volunteers. It is best known for its stability, reliability, and flexibility, and is used in many industries, including web hosting, supercomputing, and embedded systems. It is also well-suited for users who want to customize their system to their specific needs. Linux is also known for its great security features and its ability to run a variety of software, from web browsers to games. With Linux, you can create your own custom computer experience, from the desktop environment to the look and feel of the system itself.

Naviguation
-----------------------
.. figure:: /images/intro_to_linux_boot.png
    :scale: 25 %
    :align: center

    To get to Linux you will have to restart the computer and select the Linux option using the BIOS.

Ubuntu is not much different than Windows or MacOS. You can right-click to create new documents or folders, compress files, and search in specific directories. You have a Home folder with Download, Documents, Pictures, Videos, etc. You can use Firefox or Google Chrome, install software and customize the background or change your screen resolution

.. figure:: /images/intro_to_linux_desktop.png
    :scale: 25 %
    :align: center

    Linux is not much different from Windows or MacOS. There is a file explorer, web browser, text editor and everything.

.. figure:: /images/intro_to_linux_terminal.png
    :scale: 25 %
    :align: center

    You can search for tools and software by clicking in the upper-top corner.

.. figure:: /images/intro_to_linux_nautilus.jpg
    :scale: 50 %
    :align: center

    The file explorer is very similar to any OS. If you press CTRL+H you will see hidden files and folders.

.. figure:: /images/intro_to_linux_language.png
    :scale: 50 %
    :align: center

    If you intend to code, you should make sure to have access to the keyboard layout you want.


In order to learn about these functionalities, we recommend going through a tutorial `here <https://www.tutorialspoint.com/ubuntu/index.htm>`_. You can also look up YouTube tutorials to introduce features you want to know better, but be sure to check your Ubuntu version before (search for 'system info' in the applications)

Package Manager
-----------------------
Synaptic is a graphical package management tool for Debian systems. It is designed to allow users to easily install, upgrade, and remove software packages on their systems. It also provides a graphical user interface for viewing the contents of installed packages and managing the packages on the system. Synaptic is useful for users who want to install new software and keep their systems up to date. It is also useful for managing packages that have been installed from sources outside of the official Debian repositories, such as third-party repositories or manual downloads. It is easy to use and provides users with an intuitive and straightforward way to find, install, and manage software packages on their systems.

.. figure:: /images/intro_to_linux_synaptic.png
    :scale: 60 %
    :align: center

    Synaptic is installed by default on Ubuntu (any Debian OS) and will help you look for packages to install or repair mistakes you made.

This can install both libraries required for other software as well as the software itself, it is common to try to launch a new tool and be unable to install or use it until you try something like what is described in Section **Installing Stuff** (below). Synaptic is only the Graphical User Interface (GUI) for package management, but everything you do in Synaptic can be done in the Terminal.

Software Center
-----------------------
Syanptic is more powerful and was designed as a package manager. Software Center was designed as an "app-store" like program. The software center can install only one thing at a time and is a lot easier to navigate and you can read reviews and ratings.

.. figure:: /images/intro_to_linux_ubuntu_software_center.png
    :scale: 40 %
    :align: center

    The Software Center allows you to install much useful software often less related to coding and programming.


The Terminal
"""""""""""""""""""""""
The bash terminal, also known as the command line, is a powerful tool for interacting with your Linux system. It allows you to quickly execute commands, manage files and folders, and automate tasks. Bash is especially useful for system administration, scripting, and programming. 

Unlike a graphical user interface (GUI), which uses graphical elements like windows, icons, and menus, the command line requires you to type in commands to execute them. This might sound intimidating at first, but the command line can be much faster and more powerful than a GUI. Plus, with a little practice, you can become an expert in no time!

Navigating Files
-----------------------
Using the Terminal you can do anything that the GUI File Explorer can, and even more. 
The advantage of the Terminal is that operations can be automated.

**Renaming file:**
   - To rename a file in the Bash shell, you will need to use the mv command.
   - To use the mv command, you will need to specify the current name of the file and the new name you wish to give it.
   - For example, if you wanted to rename a file called “example.txt” to “newname.txt”, you would type the following command into the shell: :bash:`mv example.txt newname.txt`

**Changing directory:**
   - To change the directory you are currently located in, you will need to use the cd command.
   - To use the cd command, you will need to specify the path of the directory you wish to change to.
   - For example, if you wanted to change to the “Documents” directory, located in your home ($\sim$) directory, you would type the following command into the shell: :bash:`cd ~/Documents/`

**Copy-Pasting:**
   - To copy a file in the Bash shell, you will need to use the cp command.
   - To use the cp command, you will need to specify the file you wish to copy and the location you wish to copy it to.
   - For example, if you wanted to copy a file called “example.txt” to the “Documents” directory, located in your home directory, you would type the following command into the shell: :bash:`cp example.txt ~/Documents/`

**Ressources:**
    - Bash cheat sheet \#1 `[link] <https://www.educative.io/blog/bash-shell-command-cheat-sheet>`_
    - Bash cheat sheet \#2 `[link] <https://devhints.io/bash>`_
    - Bash cheat sheet \#3 `[link] <https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/>`_
    - Advanced concepts in Bash `[link] <https://www.pcwdld.com/bash-cheat-sheet>`_
    - Help with the :bash:`~/.bashrc` file `[link] <https://www.marquette.edu/high-performance-computing/bashrc.php>`_

Editing Text
-----------------------
The easiest way to edit text is often using the native *Text Editor* in Ubuntu, but you can install software like gEdit, Atom or Sublime for more advance text editing. When dealing with code or processing everything is in text (C++ or Python or Bash), it all depends on the extension. Raw text in a *FILE.py* is in Python and raw text in a *FILE.cpp* is C++, while *FILE.sh* is for Bash. Microsoft Word *FILE.docx*) documents can be edited using LibreOffice (LibreOffice use *FILE.odt* by default, not *FILE.docx*), but these are not suitable for coding.

So keep in mind that to edit code you need very simple software like Sublime or Atom. When not writing code, but just simple text you can use the *FILE.txt* extension, or for more advanced formatting you can try Markdown (*FILE.md*). 

If you want to edit your text file directly in the terminal, as a starting point we recommend :bash:`nano`. This will allow you to edit raw text (no formatting). It is not as intuitive as a good old GUI, but some online resources will help you with it. It is as simple as :bash:`nano ~/PATH/TO/YOUR/FILE.txt`

.. figure:: /images/intro_to_linux_nano_bashrc.png
    :scale: 65 %
    :align: center

    Nano is very useful to edit text file in the terminal and basic operation like replacing or copy-pasting lines.


**Ressources:**
    - Nano guide for novices `[link] <https://itsfoss.com/nano-editor-guide/>`_
    - Introduction to Markdown `[link] <https://www.markdownguide.org/getting-started/>`_
    - Test your Markdown online `[link] <https://stackedit.io/>`_

Installing Stuff
-----------------------
Installing packages in Linux with :bash:`apt install` is an easy and straightforward process. :bash:`apt install` is a command-line utility that is used to install, remove, and manage packages on Linux systems. It is the most commonly used package manager on Debian and Ubuntu systems.

To install a package with apt install, open up a terminal window and type in the command:
:bash:`sudo apt install <package-name>`
You will be prompted for your password to authenticate the command. After entering your password, the package will be downloaded and installed.

If you want to remove a package, you can use the command:
:bash:`sudo apt remove <package-name>`

You can also use apt to update existing packages and keep them up to date. To update all packages, you can use the command:
:bash:`sudo apt update`

Finally, you can search for packages available for installation. To do this, use the command:
:bash:`sudo apt search <package-name>`

Bash Language
"""""""""""""""""""""""
Bash Scripting
-----------------------
TODO

Advanced Commands
-----------------------
TODO

Regular Expressions
-----------------------
TODO

ComputeCanada
"""""""""""""""""""""""
ComputeCanada is a national research computing platform that provides Canadian researchers with access to powerful computing resources, storage and expertise in order to enable leading-edge research in all disciplines. It provides researchers with access to high-performance computing, cloud computing, artificial intelligence, big data and visualization resources. ComputeCanada also provides researchers with access to specialized expertise, training, support and consulting services. ComputeCanada enables researchers to accelerate their research and develop new technologies, helping to make Canada a leader in data-driven research.

You can transfer files over to ComputeCanada `[link] <https://docs.alliancecan.ca/wiki/Transferring_data>`_ and install what you need for processing. The development environment of ComputeCanada allows you to load entire modules/libraries/software easily.

.. code-block:: bash

   module load singularity/3.8
   module load nextflow/20.10.0
   module load java/11.0.2

\textbf{SLURM} (Simple Linux Utility for Resource Management) is a powerful and flexible open source workload manager and job scheduler designed specifically for supercomputers and Linux clusters. It is used to manage and allocate resources for large-scale high-performance computing jobs. SLURM allows for efficient and easy resource allocation for jobs, such as allocating nodes, CPUs, memory, and time, as well as monitoring job progress. SLURM is used by many large computing centers, including the US Department of Energy’s Oak Ridge Leadership Computing Facility.

SLURM is useful on supercomputers because it allows for efficient scheduling of resources. With SLURM, resource allocation decisions can be made quickly, ensuring that resources are always available to the jobs that need them. For example, a researcher could submit a job to a supercomputer with SLURM and the system would automatically allocate the necessary resources (e.g., nodes, CPUs, memory, and time) in order to complete the job. Additionally, SLURM can be used to monitor job progress, allowing users to keep track of their jobs’ progress and adjust resource allocation accordingly.

It is recommended to use allocated resources, you can do this by adding this to your :bash:`~/.bashrc`.

.. code-block:: bash

   export SLURM_ACCOUNT=rrg-descotea
   export SBATCH_ACCOUNT=$SLURM_ACCOUNT
   export SALLOC_ACCOUNT=$SLURM_ACCOUNT

You can launch processing using the interactive mode, (*renting* a node for a little while: `[link] <https://docs.alliancecan.ca/wiki/Running_jobs#Interactive_jobs>`_. The alternative is to dispatch tasks and let the system optimize launch: `[link] <https://docs.alliancecan.ca/wiki/Running_jobs#Use_sbatch_to_submit_jobs>`_
