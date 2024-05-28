.. _ref_setuppersocomputer:

.. role:: bash(code)
   :language: bash

Setting up your personal computer
=================================

If you intend to work on your personal computer, start by reading this page before moving on to :ref:`ref_setupcomputer`.

Choice of OS
""""""""""""

We recommend using Linux, but Mac and Windows can also be viable. If you already have a computer with Linux (or Mac) installed, proceed to the next step. If you want to install Linux on your personal computer but also want to keep Windows, you have two choices:

    1. You can dual-boot Linux and Windows by following one of the many tutorials online, such as this `one <https://www.freecodecamp.org/news/how-to-dual-boot-windows-10-and-ubuntu-linux-dual-booting-tutorial/>`_. This process can be tedious so don't hesitate to ask for help in the lab.

    2. You can use WSL2 on Windows 10 or 11. A step-by-step guide is available below to help you install WSL2.

Installing WSL
^^^^^^^^^^^^^^

If this guide is not enough or if you encounter any problems, please refer to these detailed guides for `Windows 10 <https://learn.microsoft.com/en-ca/windows/wsl/install-manual>`_ and `Windows 11 <https://learn.microsoft.com/en-ca/windows/wsl/install>`_.

#. **Enable WSL2**
    * From the Windows search bar, open the "Turn Windows Features on or off" window.
    * Scroll down to the bottom of the window and check the "Virtual Machine Platform" and "Windows Subsystem for Linux" boxes if they are not already.
    * Click on "OK" and then on "Restard now".

#. **Install Ubuntu**
    * From the Microsoft store, install your prefered version of Ubuntu. We recommend Ubuntu 22.04 LTS.

#. **Install WSL**
    * On Windows 11, simply open a Windows PowerShell and type :bash:`wsl --install`.
    * On Windows 10, open a Windows PowerShell and start by setting WSL2 as the default version of WSL:

      :bash:`wsl --set-default-version 2`

      Then, download the latest package of the "WSL2 Linux kernel update package for x64 machines" `here <https://aka.ms/wsl2kernel>`_. Double-click on the downloaded file to install it and accept everything ("Run"->"Next"->"Yes"->"Finish").

#. **Launch Ubuntu**
    * Now launch a new Ubuntu terminal by typing Ubuntu in the Windows search bar and selecting your installed version.
    * After the installation is complete, your will be asked to enter your desired username and password. This password will serve, for example, when typing a command using sudo rights.

#. **Install Windows Terminal (optional)**
    * We recommend installing Windows Terminal from Microsoft store, as it looks better, has more options and allows you to choose between your various shells (Windows PowerShell, Ubuntu 20.04, Ubuntu 22.04, etc).

#. **Create symbolic links to Windows directories (optional)**
    * Accessing Windows directories from WSL can be laborious. A nice work around is to set up symbolic links pointing to Windows in the WSL directory. For instance, you can link your “Documents” folder from Windows to a "Documents" folder in WSL, using:
    
      :bash:`ln -s /mnt/c/Users/<your Windows username>/Documents Documents`

You should now be able to use your Ubuntu terminal on Windows as if it was on Linux. You should be able to proceed to the next steps. If you have any questions that the previously cited guides can't answer, don't hesitate to ask around in the lab.

..
    #. **Enable X11 forwarding**
        * The principal drawback from WSL is the interaction with external windows, like when plotting with matplotlib or visualizing data. One workaround is to use VcXsrv.
        * Download and install `VcXsrv Windows X server <https://sourceforge.net/projects/vcxsrv/>`_.
        * Use the XLaunch.exe file to launch your xserver (it should be located in C:\\Program Files\\VcXsrv)
        * On the pop-up menu, click "Next", and "Next" again on the second window.
        * On the third window, uncheck the "Native opengl" option and check the "Disable access control" option.
        * Click "Next", then “Save configuration”, and put the file somewhere you will remember. In the future, double-click on this file to start your xserver.
        * Finally, click on "Finish".
        * If you want the xserver to open by itself when starting your computer, press the Windows key + R and enter "shell:startup". Copy the saved config file in the folder.
        * Open your Ubuntu terminal.
        * In the .profile file (gedit ~/.profile), copy-paste:

SSH and VPN
"""""""""""

    If you work from home, you might need to connect to the UdeS network for the following reasons.

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

    For further information, please refer to this `link <https://www.usherbrooke.ca/informatique/etudiants-actuels/faq/acces-a-distance-aux-serveurs-ubuntu>`_.
