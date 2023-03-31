Git
===

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


.. [1] Modified from here: https://mamchenkov.net/wordpress/2018/06/06/git-worktree-a-better-way-for-git-stash-abusers/+
.. [2] Taken here: https://buddy.works/blog/5-types-of-git-workflows