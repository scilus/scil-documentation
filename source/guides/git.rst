.. _ref_git:

Git
===

.. role:: bash(code)
   :language: bash

What is Git/Github?
-------------------
Let's say you want to save your work on internet to make sure that everything is safe if your computer breaks. Let's also say you want to share your work with other people. One answer that often comes to mind is to use Dropbox. That's good, but in the special case where your work is code (in any programming language), it is not the best solution.

For example, you're trying to develop a feature on Scilpy and your collegue is developping another feature on his own computer. 1) You don't want to save it constantly, dropbox-style. You only want to add your code once you're sure it has been correctly tested. 2) If the two of you want to add your features, we need a way to deal with conflicts if you have changed the same files. Git does that. Github, GitLab and Bitbucket are websites offering git as service in a user-friendly way.

You can find many good tutorials on internet, such as `this one <https://git-scm.com/doc>`_ on the official website. Or check `this very nice introduction <https://docs.google.com/presentation/d/1z0gsgM2Of3TIBSmJUVNPJJR6UkWZEEE_OBVYixOT8iA/edit#slide=id.g6b1c9a75fb_2_789.>`_ by Alex from our lab.

**The following sections take Scilpy as an example, but can be applied to any repositories on Github.**


For users
---------

*This section targets users who don't plan on developing code.*

.. figure:: /images/intro_to_git_link.png
   :scale: 55 %
   :align: right

You can download a repository; we say to **clone** a repository. Downloading vs cloning: when you download, it takes the code as it is then, wraps it in a zip file and downloads it all. But then, you have nothing telling you where you downloaded it from and you can't update the code. Cloning keeps the link with reference online repository and allows you to update either your local code (offline) or change the Github code (online). You will need to open a terminal and use the clone command (find the link by clicking on Github's green button *Code*): :bash:`git clone INSERT_LINK_TO_THE_REPOSITORY_TO_CLONE` 

Once cloned we recommend you to work with a stable version of the code. Often, programmers will separate their most recent (less tested) code from more stable versions by adding tags (releases) to the various versions. To use a specific version / tag / release, use :bash:`git checkout VERSION`. We expect users to remember which repository they cloned, to put the code in a appropriate folder on their computer (and know where it is), approximately when they cloned it and to remember that Scilpy constantly evolve.

If there is a bug when using the code, make sure to read the documentation, ask developers for help and if it is a real problem, raise an issue on Github.


For developers
---------------

*This section targets developers who plan on developing code.*

.. image:: /images/git_in_the_lab_remotes.png
   :scale: 25 %
   :align: right

Let's say you want to develop Scilpy. Instead of cloning Scilpy directly on your computer, you should **fork** it, i.e. copy it as one of your own repositories in your own account. On Github, you can find the button *fork* on the top right of Scilpy's repository page. Then, you can clone this copy of the repository on your computer (find the link by clicking on Github's green button *Code*): :bash:`git clone INSERT_LINK_TO_YOUR_FORKED_REPOSITORY`

The goal will be to work on your computer and save regularly your changes to **your** fork (it will automatically be named origin). We recommend immediately going inside the cloned folder (:bash:`cd scilpy` in this case) and setting up a remote named *upstream* to help link your fork to the original repository [1]_: :bash:`git remote add upstream git@github.com:scilus/scilpy.git`

By default all repositories have a main version of the code (a branch called *master* or *main*). When you are exploring new pieces of code, fixing bugs or tinkering in general you should always create a branch first (with a meaningful name) to avoid messing up your main branch with your tests: :bash:`git checkout -b my_branch`

Your main branch in **your** fork should always stay the same as the main branch in the **upstream**. A good practice is to never use :bash:`git add` or :bash:`git commit` in your main branch, only :bash:`git pull upstream master` (or main).

When working in a branch other than the main one (*master* or *main*), you should often save (update) your modifications online. Each update is called a **commit**. First, to see which files have been modified without telling Git, use :bash:`git status`. Then, to add or update a file in Git's memory, use :bash:`git add my_file`. You can also add all files that have been modified and that Git already knew about, with :bash:`git add -u`. If you check again with :bash:`git status`, everything in green will be recorded with the next command: :bash:`git commit -m "Message to explain the work I have been doing in this update"`. To send these changes to the same branch name in your forked repository, use :bash:`git push origin my_branch`.

If your modifications are useful, and you want to keep it safe, you should commit and push them. If your modifications of one branch of your own fork to be added to the real scilpy repository (upstream) could be useful to everyone and you want to share them with the rest of the world [2]_, you should consider doing a *pull request*. Only when everything is clean and tested, in the Github web interface, you can start an official pull request that will be reviewed by other members of the lab.

When that branch is accepted and merged to the master branch of the upstream, then if you update **your** own master branch of **your** fork (:bash:`git pull upstream master`), you will see the changes. You will then be able to delete safely your branch in your fork (:bash:`git branch -d my_test_branch`).

Every time you create a branch, be sure you checkout (your fork) master (:bash:`git checkout master`), then update your master with what is new *upstream* (:bash:`git pull upstream master`), finally create your branch (:bash:`git checkout -b my_branch`). This way, you will always start developing with fresh code that is up to date, this avoid conflicts and working on an already solved issue, for example. Moreover, while you develop your part of code on your branch, you might want to update the code with the latest *upstream* version. First go back to master (:bash:`git checkout master`) and update it with the *upstream* version (:bash:`git pull upstream master`). Then, go back to your branch (:bash:`git checkout my_branch`) and update it with the new *origin* version (:bash:`git pull origin master`).


For reviewers
-------------

*This section targets reviewers who plan on reviewing code.*

.. figure:: /images/git_in_the_lab_tests.png
    :scale: 65 %
    :align: right

Every once in a while you are expected to review the code of someone else. For a one time review you can **fetch** the code from *upstream* with: :bash:`git fetch upstream pull/${PR_NUMBER}/head:${DESIRED_BRANCH_NAME}` 

However, if you review a lot we recommend adding the author of the pull request (PR) as a remote, fetch the branch and checkout the code (to do every time the code changes in the pull request if multiple reviews are needed).

A few things to considering when reviewing someone else code:
    - The tests are expected to work, at the bottom of the PR (see Figure to the right)
    - Read the documentation (argparser, docstring, comments), it should be clear for non-experts
    - All changes should be needed for the bug fix or features, no modification outside of the scope of the PR
    - Fix conflicts if there is any, merge/rebase with master
    - Test it yourself to make sure you understand the change and that it works as expected
    - Be critical of the code speed, robustness, readability, etc.
    - If the PR is out of your expertise, make sure to tag someone that can help with the review


Git commands
------------

Here a list of one-line summary for Git commands
    - :bash:`git clone`: Create a local copy of a remote repository.
    - :bash:`git checkout`: Switch to a specific branch or commit.
    - :bash:`git branch`: Create a new branch.
    - :bash:`git log`: Display the commit history in the repository.
    - :bash:`git status`: Show the current state of your working directory, including changes staged, modified, or untracked.
    - :bash:`git stash`: Temporarily save uncommitted changes for later use.
    - :bash:`git add`: Stage changes in your working directory for the next commit.
    - :bash:`git commit`: Record changes made to the repo with a description.
    - :bash:`git push`: Send your local commits to a remote repository.
    - :bash:`git pull`: Retrieve changes from a remote repository and merge them into your current branch.
    - :bash:`git fetch`: Retrieve updates from a remote repository without merging them into your current branch.
    - :bash:`git merge`: Combine the changes from one branch into another.
    - :bash:`git rebase`: Reapply commits from one branch onto another, linearizing history.
    - :bash:`git remote`: Manage the list of remote repositories connected to your local repo.

Here a list of one-line summary for Git concepts
    - *a branch*: A parallel line of development in a repository.
    - *a commit*: A snapshot of the changes made to a repo, with a unique identifier and message.
    - *master/main*: The default primary branch in a Git repository, containing the latest stable version.
    - *origin*: The default name for the remote repository from which you cloned.
    - *a fork*: A copy of a repository, allowing you to make changes without affecting the original.
    - *upstream*: The original repository that a fork is based on, used to track changes from the original.
    - *hash*: A unique, fixed-length identifier generated from the content of a commit, ensuring data integrity.
    - *history*: The chronological sequence of commits in a repository, representing the evolution of a project.
    - *conflict*: A situation that occurs when two or more branches have conflicting changes to the same part of a file, requiring manual resolution.
    - *delta*: The difference between two sets of file contents, often used to represent changes between commits or branches.

.. figure:: /images/intro_to_git_organization.png
   :scale: 25 %
   :align: right

Here is a figure [1]_ with a summary of the commands that might be useful, but you can google for more information. Every action happening inside the cloud (on internet) isn't performed in command line, but with buttons on Github. Inversely, every action concerning your local computer is performed in command-line.

In Git, your working directory is the local folder containing the current state of your project files. As you make changes to these files, they are tracked by Git but not yet committed (see :bash:`git status`). 

The staging area, also known as the index, is an intermediate space where you can organize and prepare the changes you want to include in your next commit (see :bash:`git add`). By adding changes to the staging area, you're essentially telling Git which changes should be recorded in the upcoming commit (see :bash:`git commit`). Your local repository is the hidden .git folder within your working directory, where Git stores the entire version history, including all commits and branches. It is separate from the working directory, ensuring that your project's history is preserved even if you make changes or delete files in your working directory.

A remote repository is a version of your project stored on a remote server, allowing for collaboration with other developers. You can push your local commits (see :bash:`git push`) to the remote repository and pull changes made by others (see :bash:`git pull` or :bash:`git fetch`), keeping your project in sync across multiple environments.


.. [1] Modified from: https://github.com/sf-wdi-21/notes/blob/master/how-tos/github-workflow.md
.. [2] Taken from: https://buddy.works/blog/5-types-of-git-workflows