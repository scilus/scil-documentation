.. _ref_setupcomputer:

Setting up your computer
========================

We recommend using linux, but Mac can be an option. With Windows, your life will definitely be more complicated. (A popular setup is having a Linux machine in the lab and SSH-ing from a Windows machine when working from home).

The developper setup for working at the SCIL
    1. Install an up-to-date python version with development headers
    2. Create a virtual environment
    3. Install scilpy
    4. (mrtrix and mibrain)
    5. Nextflow and Docker/Apptainer

..
    Old version still makes sense but we need to figure out how we make it the easiest for new students/interns.

1. First, you should work in a virtual environment to avoid breaking your python installation. See the :ref:`ref_venvs`.

2. Install scilpy (see the :ref:`ref_scilpy` page). This will install Dipy too.

3. You may want to install Tractoflow (see :ref:`ref_tractoflow`) or our other tools (see :ref:`ref_other_pipelines`).

4. You may want to install other tools that are often useful for people in our lab (see the :doc:`here <../intro_to/explore_software>` page for MI-brain, Ants, MRtrix, FSL and Freesurfer, etc.) 

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