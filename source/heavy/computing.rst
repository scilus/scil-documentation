.. _ref_heavy_computing:

Dealing with heavy computing
============================

Using clusters
--------------

With heavy data, obviously, any programming task can be very long to execute. As an example, running the tractoflow singularity on 20 HCP subjects can easily take up to 2-3 days on an average computer. A faster way to process is to copy your data on super powerful computers and process your data directly on the distant computer. Supercomputers exist (HPC = high performance computer), which are usually not a real computer but rather a cluster of computers connected.

Generally, we could say that if you have more than 20 subjects, you could start thinking to run your job on Compute Canada. Below, you can start your job locally in the evening and let it run during the night.

Compute Canada
--------------

`Compute Canada <https://www.computecanada.ca>`_ is an example of service for clusters. An explained in the :ref:`ref_onboarding` page, you must ask for access. Here are the links to the `login page <https://ccdb.computecanada.ca>`_ and to the `wiki page <https://docs.computecanada.ca/wiki/Compute_Canada_Documentation>`_.

Our lab has access to cedar, graham or beluga. The following text takes beluga as example, but it could be either one. However, our lab has more TB and RAM on beluga.

Here is how the directories are separated into "spaces" and Compute Canada's definition of each space:

.. image:: ../images/logo_computeCanada.png
   :scale: 90 %
   :align: left

- **HOME:** While your home directory may seem like the logical place to store all your files and do all your work, in general this isn't the case - your home normally has a relatively small quota and doesn't have especially good performance for the writing and reading of large amounts of data. The most logical use of your home directory is typically source code, small parameter files and job submission scripts.
- **PROJECT:** The project space has a significantly larger quota and is well-adapted to sharing data among members of a research group since it, unlike the home or scratch, is linked to a professor's account rather than an individual user.
- **SCRATCH:** For intensive read/write operations, scratch is the best choice. This is where you can store up to 20Tb of temporary files. Remember however that important files must be copied off scratch since they are not backed up there, and older files are subject to purging. The scratch storage should therefore only be used for transient files.

Thus, when you connect (ex, with ssh), you start in a directory called USER (your username), which we also call your home. Inside, you will find:

    - projects/def-descotea: a symlink to Maxime's project space. Inside, there is one directory per user in our lab (you only have access to yours). This is where you should keep your data.
    - scratch: a symlink to your scratch space. This is where you should run your sbatch jobs (see lower for an explanation on sbatch commands).


Using Compute Canada for the first time
"""""""""""""""""""""""""""""""""""""""

1. Connect to beluga via ssh.

    .. code-block:: bash

        ssh USER@beluga.computecanada.ca

2. On your first visit, you will probably want to edit your .bashrc with your preferences.

    .. code-block:: bash

        cd # Will return you to your home
        nano .bashrc # Nano is one text editor. You might try others if you prefer.

    Here is an example. You may copy and paste this into your .bashrc.

    .. code-block:: bash

        # .bashrc

        # Source global definitions
        if [ -f /etc/bashrc ]; then
            . /etc/bashrc
        fi

        # Uncomment the following line if you don't like systemctl's auto-paging feature:
        # export SYSTEMD_PAGER=

        # User specific aliases and functions

        module load java/1.8.0_192 singularity/3.5

        #export PATH=$PATH:/home/USER/scripts  # if you have scripts
        export PATH=$PATH:$HOME/nextflow

        export SLURM_ACCOUNT=rrg-descotea
        export SBATCH_ACCOUNT=$SLURM_ACCOUNT
        export SALLOC_ACCOUNT=$SLURM_ACCOUNT

Various command lines
"""""""""""""""""""""

To understand the difference between ssh, sftp, scp, you can check the `following website <https://enterprisedt.com/products/completeftp/doc/guide/html/sftpsettings.html>`_.

    .. code-block:: bash

        # To download from beluga:
        path_beluga=/home/USER/projects/.... # Path to the data on beluga
        path_local=./                       # Path where you want to download the data (locally)
        scp USER@beluga.computecanada.ca:$path_beluga $path_local

        # Or to download with deferencing (i.e. copy reference of symlink instead of the symlink itself)
        rsync -rL USER@beluga.computecanada.ca:$path_beluga $path_local

        # To connect (then type exit to disconnect):
        ssh USER@beluga.computecanada.ca
        sftp  USER@beluga.computecanada.ca

        # Once connected, to run a job:
        sbatch my_sbatch_command_hcp.sh

        # To check your priority information
        #       - LevelFS = priority (inf = high priority).  = NormShares/EffectUsage
        #       - NormShares = proportion of Maxime's shares = What I should be using
        #       - EffectUsage = what I used. Ex, userX used 56% of ressources used in the lab.
        #       Decreases (half-time)
        sshare -l -A def-descotea_cpu

        # To check what is running
        squeue -u USER

Using sbatch
------------

Commands on distant HPC computers are ran using sbatch. You can check `tractoflow's website <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/launch.html#high-performance-computer-hpc>`_ for a sbatch example. The jobs are ran with a delay that depends on your priority as a user. The more you use ComputeCanada, the more your priority decreases. That's why it is important to be careful on the time and resources you use for each job. In your sbatch.sh file, the following options are important. If you cancel your job, your priority is not impacted. But if it succeeds or and you had overestimated the time you had to reserve, or if it crashes, it still decreases your priority. If you don't know how long a task should take, you can ask around in the lab or try to guess from information in published papers (ex, in the case of Tractoflow).

    .. code-block:: bash
    
        #!/bin/sh 
        #SBATCH --nodes=1              # --> Generally depends on your nb of subjects.
                                       # See the comment for the cpus-per-task. One general rule could be
                                       # that if you have more subjects than cores/cpus (ex, if you process 38
                                       # subjects on 32 cpus-per-task), you could ask for one more node.
        #SBATCH --cpus-per-task=40     # --> You can see here the choices. For beluga, you can choose 32, 40 or 64.
                                       # https://docs.computecanada.ca/wiki/B%C3%A9luga/en#Node_Characteristics
        #SBATCH --mem=0                # --> 0 means you take all the memory of the node. If you think you will need
                                       # all the node, you can keep 0.
        #SBATCH --time=48:00:00

Other possible options are

    .. code-block:: bash
    
        #SBATCH --mail-user=YOUR_EMAIL
        #SBATCH --mail-type=BEGIN
        #SBATCH --mail-type=END
        #SBATCH --mail-type=FAIL
        #SBATCH --mail-type=REQUEUE
        #SBATCH --mail-type=ALL

Another technique to avoid loosing priority with crashed jobs is, once connected on beluga, to run the following command:

    .. code-block:: bash

        salloc --cpus-per-task 8 --mem 16G --time 00:10:00 -A rrg-descotea

This gives you access to a node. You can then try to run your command (without sbatch) to test if it works or crashes.
