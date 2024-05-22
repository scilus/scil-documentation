.. _ref_setupcomputer:

Setting up your computer
========================

Before you can start working with the tools commonly-used or developped in the lab, you need to setup your computer. Follow this step-by-step guide to get your computer ready to work.

*This section is a work in progress. Eventually, it should cover OS choices, IDE choice, python and virtualenv installation, scilpy installation, nextflow and singularity/docker.*

We recommend using Linux, but Mac and Windows can also be viable. If you already have a computer with Linux (or Mac) installed, proceed to the next step. If you want to install Linux on your personal computer but also want to keep Windows, you have two choices:

    1) You can dual-boot Linux and Windows by following one of the many tutorials online, such as this `one <https://www.freecodecamp.org/news/how-to-dual-boot-windows-10-and-ubuntu-linux-dual-booting-tutorial/>`_. This process can be tedious so don't hesitate to ask for help in the lab.

    2) You can use WSL2 on Windows 10 or 11. A step-by-step guide is available here (*TODO add link*) to help you install WSL2.

Getting set up on super computers
"""""""""""""""""""""""""""""""""

The first use of a computing platform can be tricky but you'll get used to it. Please see the (:ref:`ref_heavy_computing`) tab for more information and for our first-use tutorial. If your goal is to use the computing platform to run Tractoflow, you will find instructions on the :ref:`ref_tractoflow` page. Else see the :ref:`ref_other_pipelines` page.

Working from home
"""""""""""""""""

    If you work from home, you might need to connect to the UdeS network. Do the following:

    1) To have access to scientific papers (ex, free access to many articles in Google scholar): See the VPN information below or go on the University's `library's website <https://www.usherbrooke.ca/biblio/trouver-des/articles-de-periodiques-revues-et-journaux/>`_ and click on "Outil de découverte" if your are logged in with your CIP (top-right corner, the connexion button).

    2) To connect to your lab computer: Use ssh or TeamViewer (see below).

VPN
    Follow `these instructions <https://www.usherbrooke.ca/services-informatiques/repertoire/reseaux/rpv/>`_ to connect through **VPN**.

    **(we might want to write a summary for English speakers)**

SSH
    1. Connect to the University's VPN.

    2. You must know your lab computer's IP address or its University code (ex: DINF-0000-00a). (Ask casius at https://casius.usherbrooke.ca/sp if you don't know).

    3. | Connect with ssh. On Linux or Mac, ssh can be simply used via the terminal. The option -X is to make sure the applications you use appear at home.
       | ``ssh -x your_cip@your_computer_IPaddress``, or
       | ``ssh -X your_cip@DINF-0000-00a.dinf.fsci.usherbrooke.ca``.

       On Windows, you can use MobaXterm. Download it, then click on Session, SSH. In Remote host, enter your IP address. In Advanced SSH settings, make sure the X11-Forwarding button is clicked.

TeamViewer (anyone still uses TeamViewer? we could replace by vscode remote ssh extension)
    You can use **screen sharing** software such as TeamViewer. You must first install TeamViewer while you are at the University and note the ID and password. Then you can install TeamViewer at home.