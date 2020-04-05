.. _ref_onboarding:

Onboarding new students
=======================

Important rooms and places
""""""""""""""""""""""""""
Chantal, Lynn, and the Faculty’s offices are important and you should know where they are. Ask someone in the lab or Maxime to guide you.


Subscriptions
"""""""""""""

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
    The code we develop (:ref:`ref_scilpy`) is offered online on `Github <https://github.com/>`_ when it's ready. It is public so you don't need an account to just look at the repository, but you will have to create an account if you will participate to scilpy's development. With an account, you can also "watch" our repo (i.e. receive emails for major changes).

Bitbucket
    The code (scilpy) is kept on `Bitbucket <https://bitbucket.org/>`_ during its development period. It is private so you need an account to access our repo. Then, email your username to Maxime. * Tip, use your @usherbrooke.ca email; you will have an academic account!

BrainData
    We deal with very heavy data and you probably don't want to keep it all on your computer. Please see the :ref:`ref_heavy_storage` tab to learn more about it. You can send an email to casius@usherbrooke.ca with Maxime in CC to have access to BrainData. Mention your CIP and that you need access to Dryade. Then, to connect to our server, in a terminal:

    .. code-block:: sh

        #Make a directory somewhere. Ex, braindata in your home
        cd ~
        mkdir braindata

        # Then connect using your username (should be your CIP)
        sshfs USER@braindata.scil.usherbrooke.ca/braindata braindata

     and to read our first-use tutorial.

Compute Canada
    This is the computing platform we use. Create an account here: `login <https://ccdb.computecanada.ca/security/login>`_. When creating your account, you will need Maxime’s info (sponsor ID). You can ask him.


Preparing your computer
"""""""""""""""""""""""

We recommand using linux, but Mac can be an option. With windows, your life will definitely be more complicated.

1. First, you should work in a virtual environment to avoid breaking your python installation. See the :ref:`ref_environments_page`.

2. Install scilpy (see the :ref:`ref_scilpy` page). This will install Dipy too.

3. You may want to install other tools that are often useful for people in our lab (see the pages for MI-brain, ants, mrtrix, fsl and freesurfer, etc.

4. Other tools exist (ex, tractoflow) but you will probably use them on Compute Canada, so see the next section.

Preparing your cluster
"""""""""""""""""""""""

The first use of a computing platform can be tricky but you'll get used to it. Please see the (:ref:`ref_heavy_computing`) tab for more information and for our first-use tutorial. If your goal is to use the computing platform to run Tractoflow, you will find instructions on the :ref:`ref_tractoflow` page. Else see the :ref:`ref_other_pipelines` page.