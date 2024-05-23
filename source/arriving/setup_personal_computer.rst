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

TODO

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
