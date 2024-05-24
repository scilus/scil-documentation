.. _ref_wsl_tuto:

Installing WSL
==============

.. role:: bash(code)
   :language: bash

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

You should now be able to use your Ubuntu terminal on Windows as if it was on Linux. You should be able to proceed with setting up your computer. If you have any questions that the previously cited guides can't answer, don't hesitate to ask around in the lab.

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
