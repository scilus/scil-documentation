Welcome
========

Important rooms and places
""""""""""""""""""""""""""
Chantal, Lynn, and the Faculty’s offices are important and you should know where they are. Ask someone in the lab or Maxime to guide you.

Suscriptions
""""""""""""

Don't hesitate to remind Maxime or his research assistants if some of the following steps were not completed.

Keys to the lab
    Maxime will ask them for you. You should receive an email.
Google Calendar
    Maxime will add you to the lab calendar. We note our lab meetings, events and other important information and we use it everyday, so you should make a habit of following it! Maxime can also add you to his personal calendar so you can follow his availabilities.  * Tip. It's easier if you have a gmail account.
Mailing list
    When Maxime wants to send a message to everyone, we either use Slack or our mailing list. Ask Maxime to add you.

Slack
    Create an account on `slack <https://slack.com>`_. We use it to communicate: it's easier to follow discussions there than by long lists of emails. To access our workspace: Ask Maxime.
Github
    The code we develop (:ref:`ref_scilpy_page`) is offered online on `Github <https://github.com/>`_ when it's ready. It is public so you don't need an account to just look at the repository, but you will have to create an account if you will participate to scilpy's development. With an account, you can also "watch" our repo (i.e. receive emails for major changes).
Bitbucket
    The code (scilpy) is kept on `Bitbucket <https://bitbucket.org/>`_ during its development period. It is private so you need an account to access our repo. Then, email your username to maxime. * Tip, use your @usherbrooke.ca email; you will have an academic account!
Working from home
    If for some reason you need to work from home but you need your installation at the University, you can use these tricks to help:

    - Follow `these instructions <https://www.usherbrooke.ca/services-informatiques/repertoire/reseaux/rpv/>`_ to connect through **VPN**. It allows to search scientific articles with the same rights as when you are at the university (ex, free access to many articles in Google scholar).
    - You can use **screen sharing** softwares such as TeamViewer.
    - You can connect through **ssh** to get your data: ssh CIP@<addresse IP>


BrainData
    We deal with very heavy data and you probably don't want to keep it all on your computer. See the Heavy Data Storage tab to learn more about it. You can send an email to casius@usherbrooke.ca with Maxime in cc to have access. Give your CIP and mention that you need access to Dryade. Then, to connect to our server, in a terminal:

.. code-block:: sh

    #Make a directory somewhere. Ex, braindata in your home
    cd ~
    mkdir braindata

    # Then connect using your username (should be your CIP)
    sshfs USER@braindata.scil.usherbrooke.ca/braindata braindata

Compute Canada
    This is the computing platform we use (see the Dealing with Heavy Computing tab). Create an account here: `login <https://ccdb.computecanada.ca/security/login>`_. When creating your account, you will need Maxime’s info (sponsor ID). You can ask him.

Preparing your computer
    See the Users of our Tools tab to see how to install everything on your computer.