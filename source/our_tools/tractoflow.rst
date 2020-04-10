.. _ref_tractoflow:

Tractoflow
==========

.. role:: bash(code)
   :language: bash

Our lab has prepared pipelines as nextflows (see the 'Nexflow' section in 'Other tools'). You can analyse all your diffusion data in only one simple script that will run a pipeline called the `Tractoflow <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/steps.html>`_, which does all the preprocessing on DWI data and T1 data and performs the wholebrain tracking.

Installing Tractoflow
*********************

    You can check the `installation guide <https://tractoflow-documentation.readthedocs.io/en/latest/installation/before_install.html>`_ on Tractoflow's website (pages before install and install). If you want to install it on Compute Canada, connect first and follow instructions in the High Performance Computer sections.

Using Tractoflow on Compute Canada
**********************************

    To learn about Compute Canada, please see the :ref:`ref_heavy_computing` page.

    To use tractoflow on a computing platform, you will find some information on Tractoflow's website, section `How to launch tractoflow <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/launch.html>`_. Here is additional, more complete instructions:

    #. Bring data to your cluster. Ex, here, on Beluga.

        .. code-block:: bash

            scp MY_DATA.zip USER@beluga.computecanada.ca:
            scp -r MY_DIR USER@beluga.computecanada.ca:  # To send a whole folder, unzipped.

    #. Connect to the cluster using ssh. Type ls and make sure that you see

        | tractoflow-x.x.x/
        | tractoflow_x.x.x_version_20xx-xx-xx.img
        | MY_DATA.zip

    #. Bring your data to your scratch directory.

        .. code-block:: bash

            mkdir scratch/Project_X
            mv MY_DATA.zip scratch/Project_X/
            cd scratch/Project_X/
            unzip MY_DATA.zip
            rm -rf MY_DATA.zip

    #. You now have all your input data ready to go for tractoflow. If you want to double-check that all the necessary files are there. Run

        .. code-block:: bash

            for a in input_data_tractoflow/*; do ls $a; done

       You should see bval  bvec  dwi.nii.gz  t1.nii.gz, as many times as you have subjects.

    #. Nextflow will need to find your data in the scratch. As explained on Tractoflow's website (section How to launch your data), create a file beluga.conf in your project (ex, using nano), which contains these 2 lines.

        .. code-block:: bash

            singularity.runOptions="--bind /lustre04/scratch/USER/"
            process.executor='ignite'


    #. If you want to have an idea of the b-values in your protocol because you are not sure (this is useful to know to set the dti_shells and fodf_shells in your future tractoflow command):

        .. code-block:: bash

            for a in input_data_tractoflow/*; do cat $a/bval; done

    #. Tractoflow is 100% reproducible if you re-use in the future the SAME code and SAME container image (singularity). Hence, copy them locally in your project to SAVE them in the future.

        .. code-block:: bash

            cd ~/projects/def-descotea/USER
            mkdir Project_X
            cd Project_X
            cp ~/tractoflow_*.img .
            cp -r ~/tractoflow-* .

    #. Now, we are ready to run tractoflow. Most important questions you should ask yourself:

        - What shells (if you have multi-shell data) will I use to compute DTI metrics? *Typically: b < 1200*
        - What shells (if you have multi-shell data) will I use to compute fODFs & metrics? *Typically: b>700 and the b0.*
        - Do I want to fix the fiber response function (FRF) or compute the mean FRF for my group? *Typically: ?*
        - What seeding strategy do you want for PFT tracking? Interface seeding or WM seeding? *Depends on your project. Ex, for a connectomics study, interface seeding is better.*
        - How many seeds do you want? (or how many streamlines you wish to have in the final tractogram?) *Typically: ~2,000,000 - 3,000,000 streamlines. To calculate the number of seeds per voxel, you can use an approximation. Ex: on a test subject, we found 260k voxels of the wm-gm interface, from which we will seed. 260,000*15 = 3.9M seeds will be launched. Hopefully, this should lead to 2.5M-3.5M streamlines in the final tractogram.*

       If any of the above four questions are puzzling or do not make sense, go back to your notes, readings, and courses. You don’t understand what you are about to launch! Or see Max or someone in the SCIL for help and an important discussion.

       For example, we could launch the following command. However, **don't run it now**, we will actually use a sbatch (see lower).

        .. code-block:: bash

            # This would run tractoflow with the following parameters:
            #   - Dti_shells 0 and 1500, Fodf_shells 0 and 1500.
            #   - Fix the FRF to (15,4,4) x 10^-4 mm2/s
            #   - Interface seeding
            #   - nbr_seeds 15.
            nextflow -c ../beluga.conf run ../tractoflow-*/main.nf --root ../input_data_tractoflow \
                -with-singularity ../tractoflow_*.img -resume -with-report report.html \
                --dti_shells "0 1500" --fodf_shells "0 1500" --step 0.5 --nbr_seeds 15 \
                --wm_seeding false --mean_frf false --set_frf true

    #. Before launching your command for real, let's test it quickly using an interactive node. You ask access to an interactive node doing this:

        .. code-block:: bash

            cd ~/scratch/Project_X
            mkdir output_tractoflow
            cd output_tractoflow

            salloc -c 32 --mem 32G --time 00:10:00 -A def-descotea

            # Wait for the node to be allocated to you.
            # If our lab lacks priority and it is too long, you can try with -c 16 --mem 16Gb.
            # When allocation is granted, you should see:
            #   salloc: Pending job allocation xxx
            #   salloc: job xxx queued and waiting for resources
            #   salloc: job xxx has been allocated resources
            #   salloc: Granted job allocation xxx
            #   salloc: Waiting for resource configuration
            #   salloc: Nodes yyym are ready for job

            # Then type the tractoflow command with --help at the end. Tractoflow's help should be printed.

            # Then, you may type the real command. Make sure it starts running. Once sure that it found the data, the img, the code, you can kill it by pressing ctrl-c.

       If it fails:

         - Is the data binding correctly (see point 5)?
         - If one process fails, you should see a warning such as ``[11/53e26e] NOTE: Process `Bet_Prelim_DWI (101309)` terminated with an error exit status (127) -- Execution is retried (3)``. You can then check in the associated folder's log to see the error. For example:

         .. code-block:: bash

            ls -a work/11/53e26e*/  # Check that files are there
            cat work/11/53e26e*/.command.log  # Check the error

    #. Last decision to take on the cluster: Do you need 1 node or multiple nodes? Beyond 20 subjects or so, we recommend using multiple nodes. See the HPC part of tractoflow's `launch page <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/launch.html>`_. Depending on the cluster you are using (beluga, cedar, etc.), you have access to different types of nodes. Keeping the option "mem=0" in your sbatch (see next step) means you accept any node. If your data is very heavy (ex, HCP data), you might need to restric to the nodes with more RAM. See the `memory section here <https://docs.computecanada.ca/wiki/Running_jobs#Memory>`_ for more information.

    #. We have all the ingredients to prepare the final sbatch. Here, we ask for 4 nodes, with 32 threads each and 116Gb of RAM each (see the -with-mpi option). Create a file cmd_my_tractoflow.sh with the following.

        .. code-block:: bash

            #!/bin/sh
            #SBATCH --mail-user=YOUR_EMAIL
            #SBATCH --mail-type=BEGIN
            #SBATCH --mail-type=END
            #SBATCH --mail-type=FAIL
            #SBATCH --mail-type=REQUEUE
            #SBATCH --mail-type=ALL

            #SBATCH --nodes=2
            #SBATCH --cpus-per-task=32
            #SBATCH --mem=0
            #SBATCH --time=24:00:00

            export NXF_CLUSTER_SEED=$(shuf -i 0-16777216 -n 1)

            srun (copy your nextflow command from point 9) -with-mpi

    #. Finally launch your sbatch! Yeah!

        .. code-block:: bash

            sbatch -A def-descotea cmd_my_tractoflow.sh

            squeue -u USER  # To check if it has been launched

            exit # To quit beluga

        You will receive an email when your command is launched (if you provided it in step 11). If you want to supervise the results while it runs, you should find a file such as slurm-6635828.out. It is the equivalent of what would be printed in your terminal if you ran it directly. You can download it with scp or simply look at it using 'cat slurm-6635828.out'.

        .. note:: It is normal to see some failed tasks. The way it works, many jobs are started at the same time, and it may cause some scheduling errors. As long as some jobs succeed, you can let it run.

    #. We recommend doing something like this to save results, scripts and container

        .. code-block:: bash

            mkdir final_results
            mkdir final_results/containers/
            mkdir final_results/scripts
            cp output_tractoflow/cmd_*.sh final_results/scripts/
            cp output_tractoflow/beluga.conf final_results/scripts/
            cp -rL output_tractoflow/results final_results/tractoflow
            cp -rL qa-nf/results_QA final_results/qa-tractoflow

            mv *img final_results/containers/
            cp *.txt final_results/scripts/

            # If you are sure to be done, uncomment following line
            # rm -rf input_* output_*

Using config files
******************

.. note::

    These instructions are particularly useful if you are trying to preprocess HCP data (Human Connectome Project). The data (as found for instance on BrainData, see :ref:`ref_heavy_storage`), is not totally raw and should not be used directly in tractoflow. We have prepared special parameters for such cases. They are kept in a nextflow.config file.

The tractoflow command can also be ran with most options listed in a config file such as `this one <https://github.com/scilus/tractoflow/blob/master/nextflow.config>`_. You simply have to keep the nextflow.config file in the directory from where you run your command.
