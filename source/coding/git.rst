Git
===

.. role:: bash(code)
   :language: bash

If you do not know what is Git, you should visit the page (CROSSREF when done) to learn about the basic concepts and commands of Git. This page is specifically to learn how we use Git in the lab, what we expect and how you can contribute.

For users
---------

*If you are only a user and you don't plan on developing the code:*

You can download a repository; we say to **clone** a repository. Downloading vs cloning: when you download, it takes the code as it is then, wraps it in a zip file and downloads it all. But then, you have nothing telling you where you downloaded it from and you can't update the code. Cloning keeps the link with git and allows you to update. You will need to open a terminal and use the :bash:`git clone` command. You can find the address by clicking on Github's green button *clone repository*.

Once cloned we recommend either using a tag (a release) with the :bash:`git checkout` to ensure a stable version of the code. We expect users to remember which repository the cloned, to put the code in a appropriate folder on their computer (and know where it is), approximately when they cloned it and to remember that Scilpy constantly evolve.

If there is a bug when using the code, make sure to read the documentation, ask developers for help and if it is a real problem, raise an issue on Github.

For developers
---------------

.. image:: /images/git_in_the_lab_remotes.png
   :scale: 25 %
   :align: right

Our standards are based on recommendations you can find anywhere on the web. Let's say you want to develop Scilpy. Instead of cloning Scilpy directly on your computer, you should **fork** it, i.e. copy it as one of your own repositories in your own account. On Github, you can find the button *fork* on the top right of Scilpy's repository page. Then, you can clone this copy of the repository (link to your account) on your computer.

The goal will be to work on your computer and save your changes to your fork (origin) (don't forget to save regularly!). We recommend immediately setting up a remote named *upstream* to help link your fork to the original repository: :bash:`git remote add upstream git@github.com:scilus/scilpy.git` [1]_.

By default all repositories have a main version of the code (a branch called *master* or *main*). When you are exploring new pieces of code, fixing bugs or tinkering in general you should always create a branch first (with a meaningful name) :bash:`git checkout -b my_branch`.

If your modifications are useful, and you want to keep it safe, you should commit and push them. If your modifications could be useful to everyone and you want to share it with the rest of the world [2]_, you should consider doing a *pull request*. Only when everything is clean and tested, in the Github web interface, you can start an official pull request that will be reviewed by other members of the lab.

.. image:: /images/git_in_the_lab_features.png
    :scale: 50 %
    :align: left

Generally, you should keep your master equal to the upstream's master. You should develop each feature in a separated branch. When you are ready to send your code to the upstream (pull request), it is usually not a good practice to send the work from your master branch, it should come from a branch with this purpose.

Every time you create a branch, be sure you checkout (your fork) master (:bash:`git checkout master`), then update your master with what is new *upstream* (:bash:`git pull upstream master`), finally create your branch (:bash:`git checkout -b my_branch`. This way, you will always start developing with fresh code that is up to date, this avoid conflicts and working on an already solved issue, for example.

For reviewers
-------------

Every once in a while you are expected to review the code of someone else. For a one time review you can use: :bash:`git fetch upstream pull/${PR_NUMBER}/head:${DESIRED_BRANCH_NAME}` to get the code. However, if you review a lot we recommend adding the author of the pull request (PR) as a remote, fetch the branch and checkout the code (to do every time the code change in the pull request if multiple reviews are needed).

A few things to considering when reviewing someone else code:
    - The tests are expected to work, at the bottom of the PR (see Figure below)
    - Read the documentation (argparser, docstring, comments), it should be clear for non-experts
    - All changes should be needed for the bug fix or features, no modification outside of the scope of the PR
    - Fix conflicts if there is any, merge/rebase with master
    - Test it yourself to make sure you understand the change and that it works as expected
    - Be critical of the code speed, robustness, readability, etc.
    - If the PR is out of your expertise, make sure to tag someone that can help with the review

.. figure:: /images/git_in_the_lab_tests.png
    :scale: 60 %
    :align: left

.. [1] Modified from: https://mamchenkov.net/wordpress/2018/06/06/git-worktree-a-better-way-for-git-stash-abusers/
.. [2] Taken from: https://buddy.works/blog/5-types-of-git-workflows

PS: This section applies to Scilpy (in Python), but also to any repositories for Flows and Docker/Singularity, but also this ReadTheDocs. We use Git for a lot more than the Python libraries.
