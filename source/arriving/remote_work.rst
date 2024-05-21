.. _ref_remote_work:

Working from home
=================

If you work from home, you might need to connect to the UdeS network. Do the following:

1) To have access to scientific papers (ex, free access to many articles in Google scholar): See the VPN information below or go on the University's `library's website <https://www.usherbrooke.ca/biblio/trouver-des/articles-de-periodiques-revues-et-journaux/>`_ and click on "Outil de découverte" if your are logged in with your CIP (top-right corner, the connexion button).

2) To connect to your lab computer: Use ssh or TeamViewer (see below).

VPN
    Follow `these instructions <https://www.usherbrooke.ca/services-informatiques/repertoire/reseaux/rpv/>`_ to connect through **VPN**.

    .. Comment. We might want to write a summary for English speakers.

SSH
    1. Connect to the University's VPN.

    2. You must know your lab computer's IP address or its University code (ex: DINF-0000-00a). (Ask casius at https://casius.usherbrooke.ca/sp if you don't know).

    3. | Connect with ssh. On Linux or Mac, ssh can be simply used via the terminal. The option -X is to make sure the applications you use appear at home.
       | ``ssh -x your_cip@your_computer_IPaddress``, or
       | ``ssh -X your_cip@DINF-0000-00a.dinf.fsci.usherbrooke.ca``.

       On Windows, you can use MobaXterm. Download it, then click on Session, SSH. In Remote host, enter your IP address. In Advanced SSH settings, make sure the X11-Forwarding button is clicked.

TeamViewer
    .. Anyone still uses TeamViewer? we could replace by vscode remote ssh extension

    You can use **screen sharing** software such as TeamViewer. You must first install TeamViewer while you are at the University and note the ID and password. Then you can install TeamViewer at home.