.. _ref_onboarding:

Onboarding new students
=======================

Important rooms and places
""""""""""""""""""""""""""
Chantal Proulx, Marie-Pier Côté and generally the `Faculty’s offices <https://www.usherbrooke.ca/informatique/nous-joindre/personnel>`_ are important and you should know where they are. Ask someone in the lab or Maxime to guide you.

Subscriptions
"""""""""""""

Don't hesitate to remind Maxime or his research assistants if some of the following steps were not completed.

Keys to the lab
    Maxime will ask them for you. You should receive an email.

Google Calendar + Teams Calendar
    Maxime will add you to the lab calendar. We note our lab meetings, events and other important information and we use it everyday, so you should make a habit of following it! Maxime can also add you to his personal calendar so you can follow his availabilities.  * Tip. It's easier if you have a gmail account.

Mailing list
    When Maxime wants to send a message to everyone, we either use Teams or our mailing list. Ask Maxime to add you.

Teams
    We use Microsoft Teams as means of communication. You can use your CIP and university's password to connect. You can ask Maxime to add you to the SCIL's "team". Then, you can explore the various conversations, called "channels". When lab meetings are online, you can join them via the "General" channel. Also, we encourage you to explore the videos in the video tab from the General channel. You can find there the recording of previous lab meetings, videos of Max's dMRI class and more.

Github
    The code we develop (:ref:`ref_scilpy`) is offered online on `Github <https://github.com/>`_ when it's ready. It is public so you don't need an account to just look at the repository, but you will have to create an account if you will participate to scilpy's development. With an account, you can also "watch" our repo (i.e. receive emails for major changes).

Bitbucket
    `Bitbucket <https://bitbucket.org/>`_ is an alternative to Github if you want to keep your code private, you might want to use it eventually. \*Tip, use your @usherbrooke.ca email; you will have an academic account!

BrainData
    We deal with very heavy data and you probably don't want to keep it all on your computer. See the Heavy Data Storage tab to learn more about it. You can go to https://casius.usherbrooke.ca/sp to communicate with Casius to have access. Give your CIP, mention Maxime Descoteaux and mention that you need access to Dryade. Then, to connect to our server, in a terminal:

    .. code-block:: sh

        # Make a directory somewhere. Ex, braindata in your home
        cd ~
        mkdir braindata

        # Then connect using your username (should be your CIP)
        sshfs USER@braindata.scil.usherbrooke.ca:/braindata braindata

Compute Canada
    This is the computing platform we use (see the Dealing with Heavy Computing tab). Create an account here: `login <https://ccdb.computecanada.ca/security/login>`_. When creating your account, you will need Maxime’s info (sponsor ID). You can ask him.

Preparing your computer
"""""""""""""""""""""""

We recommend using linux, but Mac can be an option. With Windows, your life will definitely be more complicated.

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

SSH
    1. Connect to the University's VPN.

    2. You must know your lab computer's IP address or its University code (ex: DINF-0000-00a). (Ask casius at https://casius.usherbrooke.ca/sp if you don't know).

    3. | Connect with ssh. On Linux or Mac, ssh can be simply used via the terminal. The option -X is to make sure the applications you use appear at home.
       | `ssh -x your_cip@your_computer_IPaddress`, or
       | `ssh -X your_cip@DINF-0000-00a.dinf.fsci.usherbrooke.ca`.

       On Windows, you can use MobaXterm. Download it, then click on Session, SSH. In Remote host, enter your IP address. In Advanced SSH settings, make sure the X11-Forwarding button is clicked.

TeamViewer
    You can use **screen sharing** software such as TeamViewer. You must first install TeamViewer while you are at the University and note the ID and password. Then you can install TeamViewer at home.