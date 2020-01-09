Dealing with heavy computing
============================

Using clusters
---------------

With heavy data, obviously, any programming task can be very long to execute. As an example, running the tractoflow singularity on HCP data can easily take up to ...(??) on an average computer. A faster way to process is to copy your data on super powerful computers and process your data directly on the distant computer. Supercomputers exist (HPC = high performance computer), which are usually not a real computer but rather a cluster of computers connected

Compute Canada
---------------

`Compute Canada <https://www.computecanada.ca>`_ is an example of service for clusters. An explained in the Welcoming page, you must ask for access. Here are the links to the `login page <https://ccdb.computecanada.ca>`_ and to the `wiki page <https://docs.computecanada.ca/wiki/Compute_Canada_Documentation>`_.

Our lab has access to CEDAR. Here is how the directories are separated. When you connect (ex, with ssh), you land in a directory called USER (your username), which we can also call your home. Inside, you will find:

    - projects/def-descotea: a symlink to Maxime's project space. Inside, there is one directory per user in our lab (you only have access to yours). This is where you should keep your data.
    - scratch: a symlink to your scratch space. This is where you should run your sbatch jobs.

Here is how Compute Canada defines each space:

.. image:: ../images/logo_computeCanada.png
   :scale: 90 %
   :align: left

- **HOME:** While your home directory may seem like the logical place to store all your files and do all your work, in general this isn't the case - your home normally has a relatively small quota and doesn't have especially good performance for the writing and reading of large amounts of data. The most logical use of your home directory is typically source code, small parameter files and job submission scripts.
- **PROJECT:** The project space has a significantly larger quota and is well-adapted to sharing data among members of a research group since it, unlike the home or scratch, is linked to a professor's account rather than an individual user.
- **SCRATCH:** For intensive read/write operations, scratch is the best choice. Remember however that important files must be copied off scratch since they are not backed up there, and older files are subject to purging. The scratch storage should therefore only be used for transient files.

See below for the command line to connect to cedar. To understand the difference between ssh, sftp, scp, you can check the `following website <https://enterprisedt.com/products/completeftp/doc/guide/html/sftpsettings.html>`_.

Commands on distant HPC computers are ran using sbatch. You can check `tractoflow's website <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/launch.html#high-performance-computer-hpc>`_ for a sbatch example. The jobs are ran with a delay that depends on your priority as a user. The more you use ComputeCanada, the more your priority decreases. That's why it is important to be careful on the time and resources you use for each job. In your sbatch.sh file, the following options are important and here are how recommandations:

.. code-block:: bash

    #SBATCH --nodes=1               # --> We recommand ???
    #SBATCH --cpus-per-task=32      # --> We recommand ???
    #SBATCH --mem=0                 # --> We recommand ???
    #SBATCH --time=48:00:00         # --> We recommand ???

Finally the command lines are:

.. code-block:: bash

    # To download from cedar:
    path_cedar=/home/USER/projects/.... # Path to the data on cedar
    path_local=./                       # Path where you want to download the data (locally)
    scp USER@cedar.computecanada.ca:$path_cedar $path_local

    # Or to download with deferencing (i.e. copy reference of symlink instead of the symlink itself)
    rsync -rL USER@cedar.computecanada.ca:$path_cedar $path_local

    # To connect (then type exit to disconnect):
    ssh USER@cedar.computecanada.ca
    sftp  USER@cedar.computecanada.ca

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
