Git
===

What are git/Github/Bitbucket?
------------------------------

Let's say you want to save your work on internet to make sure that everything is safe if your computer breaks. Let's also say you want to share your work with other people. One answer that often comes to mind is to use Dropbox. That's good, but in the special case where your work is code (in any programming language), it is not the best solution.

Ex: you're trying to develop a feature on, ex, scilpy, and your collegue is developping another feature on his own computer. 1) You don't want to save it constantly, dropbox-style. You only want to add your code once you're sure it has been correctly tested. 2) If the two of you want to add your features, we need a way to deal with conflicts if you have changed the same files. Git does that. Github and bitbuckets are two websites offering git as service in a user-friendly way.

You can find many good tutorials on internet, such as `this one <https://git-scm.com/doc>`_ on the official website.

How we use git in the lab
-------------------------

*If you are only a user and your don't plan on developping the code:*

    You can download a repository; we say to **clone** a repository. Downloading vs cloning: when you download, it takes the code as it is then, wraps it in a zip file and downloads it all. But then, you have nothing telling you where you downloaded it from and you can't update the code. Cloning keeps the link with git and allows you to update. Simply go in a terminal in the directory where you want to install some repository and enter: git clone https://my_repo.git. You can find the address by clicking on Github's green button "clone repository".

    .. image:: /images/git1_modifiedEm.png
       :scale: 25 %
       :align: right

*If you plan on developping code, here is how we suggest you do:*

    Our standards are based on recommandations you can find anywhere on the web. Let's say you want to develop scilpy. Instead of cloning scilpy directly on your computer, you should **fork** it, i.e. copy it as one of your own repository in your own account. On Github, you can find the button "fork" on the top right of scilpy's repository page. You can clone this repository on your computer (see last paragraph). This leaves you with three connected repositories (see Fig [1]_).

    * **upstream**; the first official repository. On internet.
    * **origin**: your forked repository from which you cloned. On internet.
    * **local**: files for which git is aware. On your computer.
    * **workspace**: files that you have created or modified on your computer without telling git.

    The goal will be to work on your computer and save your changes to your fork (origin) (don't forget to save regularly!), and, only when everything is clean and tested, add your work to the upstream through an official pull request that will be thoroughly reviewed by other members of the lab.

    .. image:: /images/git3.png
       :scale: 45 %
       :align: left

    Before giving code examples, there is one last aspect to introduce: **branches**. Each of the upstream, origin and local can be separated into branches, that act as versions of your code, as on the figure [2]_. The main version is always called the **master**. On Github, you can see the code for different branches by clicking on the branch button. On your computer, you can only see one branch at the time. To switch to another branch, everything must be saved on the current branch to avoid loosing work. Usually, the branches on your local repo and in your fork (origin) have the same name to avoid confusion.

    Generally, you should keep your master equal to the upstream's master. You should develop each feature in a separated branch. When you are ready to send your code to the upstream (pull request), it is usually not a good practice to send the work from your master branch, it should come from a branch with this purpose.


Summary of git commands
-----------------------

    Here is a figure [3]_ with a summary of the commands that might be useful, but you can google for more information. Every action happening inside the cloud (on internet) isn't performed in command line, but with buttons on Github. Inversely, every action concerning your local computer is performed in command line.

    .. image:: /images/git2_modifiedEm.png
       :scale: 40 %
       :align: right

Setting up everything the first time
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

    # Cloning the code
    git clone $link_to_myFork
    cd myFork

    # Telling git who are the upstream and origin
    git remote add upstream $link_to_upstream
    git remote add origin $link_to_myFork # Should be set automatically
    git remote -v # To verify everything.

    # Creating branches
    git branch myBranch1 # create it
    git checkout myBranch1 # switch on it
    git checkout -b myBranch2 # create AND switch
    # Note that here, myBranch2 would be a copy of myBranch1.
    # If instead you want to start from the master, switch to your master branch first.

Downloading updates
^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

    # From the origin to both your local repo and your workspace:
    git pull origin master # master or any branch you want to update.
                           # Note that this is equivalent to git fetch + git merge.

    # From the upstream to your local repo
    git pull upstream master

    # From the upstream to your forked repo
    # There is no way to do this direclty. You can update your local repo and
    # send the update back up to your forked repo
    git push origin master

    # Updating one branch on your computer with the updates from the master:
    # Update master. Then:
    git rebase master myBranch


Uploading your changes
^^^^^^^^^^^^^^^^^^^^^^

.. image:: /images/git5.jpeg
   :scale: 80 %
   :align: right

Each update is called a **commit**. See figure [4]_.

.. code-block:: bash

    # From the workspace to your local repo:
    git status # To see which files have been modified without telling git
    git add myFile  # To add or update a file in git's memory.
    git add -u      # To add all files that have been modified, but that git already knew
    git status      # If you check again, everything in green will be recorded with the next command:
    git commit -m "Message to explain the work I have been doing in this update"

    # From the local repo to your forked repo
    git push origin myBranch  # Will automatically send it to the same branch name in your forked repo.

    # From your forked repo to the upstream repo:
    # Use the Pull Request button on internet

    # From your local repo to the upstream repo:
    # DON'T DO THAT. Didn't you see that there is no such arrow on the figure!


.. image:: /images/git4.png
   :scale: 75 %
   :align: right

Merging branches
^^^^^^^^^^^^^^^^

Figure: [5]_.

.. code-block:: bash

    # Technique 1: merge. To merge branch2 (pink) into branch1 (yellow):
    git checkout branch1
    git merge branch2

    # Technique 2: rebase
    git rebase branch1 branch2

.. [1] Modified from here: https://mamchenkov.net/wordpress/2018/06/06/git-worktree-a-better-way-for-git-stash-abusers/+
.. [2] Taken here: https://buddy.works/blog/5-types-of-git-workflows
.. [3] Modified from here: https://github.com/sf-wdi-21/notes/blob/master/how-tos/github-workflow.md
.. [4] https://medium.com/tech-and-the-city/changing-a-super-old-git-commit-history-20346f709ca9
.. [5] Taken here: http://www.differencebetween.net/technology/difference-between-git-rebase-and-merge/