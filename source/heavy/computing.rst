Dealing with heavy computing
============================

Using clusters
---------------

With heavy data, obviously, any programming task can be very long to execute. As an example, running the tractoflow singularity on HCP data can easily take up to ...(??) on an average computer. A faster way to process is to copy your data on super powerful computers and process your data directly on the distant computer. Supercomputers exist (HPC = high performance computer), which are usually not a real computer but rather a cluster of computers connected

Compute Canada
---------------

Compute Canada is an example of service for clusters.

.. code-block:: bash

    # To connect:
    ssh renaulde@cedar.computecanada.ca


    # To download from:
    path_cedar=/home/renaulde/projects/def-descotea/meditation_input_data.tar.gz
    path_local=./
    scp renaulde@cedar.computecanada.ca:$path_cedar $path_local

    # Or connect with sftp
    # Or to download with deferencing (copy reference of symlink instead of symlink
    rsync -rL renaulde@cedar.computecanada.ca:$path_cedar $path_local


    # To run something:
    sbatch cmd_tractoflow_hcp.sh


    # To check your priority information
    #       - LevelFS = priority (inf = high priority).     = NormShares/EffectUsage
    #       - NormShares = proportion of Maxime's shares = What I should be using
    #       - EffectUsage = what I used. Ex, userX used 56% of ressources used in the lab.
    #       Decreases (half-time)
    sshare -l -A def-descotea_cpu


    # To check what is running
    squeue -u renaulde
