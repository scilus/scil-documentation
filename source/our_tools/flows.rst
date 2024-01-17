.. _ref_flow:

Flows
=====

.. role:: bash(code)
   :language: bash

Here we'll look at how to move from the raw diffusion imaging data to the tractography metrics, whether for global visualization or at the scale of the invididual, using flows created by our laboratory.

Requirements
************

* For this test, there is a necessity that you have a Nextflow version between 19.04.2 and 21.12.1, the various git flows cloned (tractoflow, rbx_flow, tractometry_flow) and have a container installed.
* For Nextflow and tractoflow you can check the `installation guide <https://tractoflow-documentation.readthedocs.io/en/latest/installation/install.html>`_ from the tractoflow documentation. Otherwise, the installation of Nextflow is also presented `here <https://scil-documentation.readthedocs.io/en/latest/intro_to/explore_nextflow.html#installation>`_.
* To `git clone <https://scil-documentation.readthedocs.io/en/latest/intro_to/explore_git.html#summary-of-git-commands>`_ the different flows you can follow these links:

   - `tractoflow <https://github.com/scilus/tractoflow>`_
   - `rbx_flow <https://github.com/scilus/rbx_flow>`_
   - `tractometry_flow <https://github.com/scilus/tractometry_flow>`_

* I recommend that you store the various pipelines in places that are easy to find and whose direction you know.
* Finally, you will need a container as Apptainer or Singularity. The whole documentation about it and how to install it is `here <https://scil-documentation.readthedocs.io/en/latest/intro_to/explore_virtual_machines.html#singularity>`_.

Initialization
**************

#. Open a terminal and navigates to a working folder you create for the test or use this command:

    .. code-block:: bash

        mkdir -p flows_tutorial_1.6.0 && cd flows_tutorial_1.6.0

#. To make it easier to write nextflow commands, we recommend that you create a shortcut to the file containing your flows.

    .. code-block:: bash

        export FLOW_DIR="/PATH/TO/YOUR/FLOWS/"
        #Example <export FLOW_DIR="/home/user/libraries/flows/">


#. If it's your first time to use our flow we recommand you to use this set of data who has been prepared for this introduction.

    .. code-block:: bash

        mkdir data_tuto_1.6.0
        curl https://nextcloud.computecanada.ca/index.php/s/jtzgL352cxpxxzt/download -o data_tuto_1.6.0/data_tuto_1.6.0.zip
        unzip -qq data_tuto_1.6.0/data_tuto_1.6.0.zip -d data_tuto_1.6.0/

#. Also, you can download the singularity "container_scilus_1.6.0.sif" necessary for this test with this command:

    .. code-block:: bash

        curl https://nextcloud.computecanada.ca/index.php/s/NijdKTP7WWbP7Na/download -o containers_scilus_1.6.0.sif

#. Finally, create the different directions for the different flows according to the structure of the inputs required for each.

    .. code-block:: bash

        for i in data_tuto_1.6.0/sub-*; do mkdir -p tractoflow_test/raw/$(basename $i);done
        for i in data_tuto_1.6.0/sub-*; do mkdir -p RBx_flow_test/raw/$(basename $i);done
        for i in data_tuto_1.6.0/sub-*; do mkdir -p tractometry_flow_test/raw/$(basename $i); done

Tractoflow
**********

#. Add the data needed to launch tractoflow from downloaded data.

    .. code-block:: bash

        for i in data_tuto_1.6.0/sub-*; do cp ${i}/* tractoflow_test/raw/$(basename $i)/; done

.. note::

    The data are composed of 3 subjects and each subject contains 7 files: aparc+aseg.nii.gz, bval, bvec, dwi.nii.gz, rev_b0.nii.gz, t1.nii.gz, wmparc.nii.gz.
    By default only bval, bvec, dwi.nii.gz, t1.nii.gz are necessary to run tractoflow. 
    But here we're using tractoflow ABS, so aparc+aseg.nii.gz, rev_b0.nii.gz, and wmparc.nii.gz are required.

#. Run tractoflow (this can take a long time).

    .. code-block:: bash

        nextflow ${FLOW_DIR}/tractoflow/main.nf --input tractoflow_test/raw --local_nbr_seeds 1 --run_eddy False \
         --run_topup False --output_dir tractoflow_test/results_tf -profile ABS -with-singularity ./containers_scilus_1.6.0.sif \
         -with-report tractoflow_test/report.html -w tractoflow_test/work -resume

 Parameters:
  - :bash:`--input`: direction of our data
  - :bash:`--local_nbr_seeds`: number of seeds related to the seeding type param
  - :bash:`--run_eddy`: activate or not eddy
  - :bash:`--run_topup`: activate or not topup
  - :bash:`--output_dir`: direction where results will be generate
  - :bash:`-profile ABS`: choose the profile TractoFlow-ABS (Atlas Based Segmentation)
  - :bash:`-with-singularity`: direction of singularity we want to use
  - :bash:`-with-report`: generate a report a the end of the command
  - :bash:`-w`: direction where work will be generate
  - :bash:`-resume`: use the results already created in the work if the command has already been executed

Here, tractoflow is set to be as fast as possible if you want to check more options run the command :

    .. code-block:: bash
        
        nextflow ${FLOW_DIR}/tractoflow/main.nf --help

Or you can check the documentation from tractoflow documentation `here <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/options.html>`_.
    
.. warning::
    Once tractoflow is launched, a large number of files are created. Be careful, the files in results are only symlinks to the work. Do not delete your work!

References :
    * Theaud et al. (2020). TractoFlow: A robust, efficient and reproducible diffusion MRI pipeline leveraging Nextflow & Singularity. `<https://doi.org/10.1016/J.NEUROIMAGE.2020.116889>`_

Rbx_flow
********

For the RBx_flow step, we are only interested in two files: the local tracking file and the fractional anisotropy (fa) from tractoflow.

#. Import local tracking and fa files to RBx_flow inputs.

    .. code-block:: bash

        for i in tractoflow_test/results_tf/sub-*; do cp ${i}/*/*fa.nii.gz RBx_flow_test/raw/$(basename $i)/; done
        for i in tractoflow_test/results_tf/sub-*; do cp ${i}/*/*tracking*.trk RBx_flow_test/raw/$(basename $i)/; done

#. Download an atlas and config files for RBx_flow, in our case using the atlas and config in zenodo. However, the RBx_flow input architecture must be retained.

    .. code-block:: bash

        mkdir atlas
        curl https://zenodo.org/records/7950602/files/atlas.zip?download=1 -o atlas/atlas.zip
        curl https://zenodo.org/records/7950602/files/config.zip?download=1 -o atlas/config.zip
        unzip -qq atlas/atlas.zip -d atlas/
        unzip -qq atlas/config.zip -d atlas/

#. Run RBx_flow.

    .. code-block:: bash

        nextflow ${FLOW_DIR}/rbx_flow/main.nf --input RBx_flow_test/raw --atlas_directory atlas \
         -with-singularity ./containers_scilus_1.6.0.sif -w RBx_flow_test/work -resume

Parameters:
  - :bash:`--input`: direction of our data
  - :bash:`--atlas_directory`: direction of our atlas
  - :bash:`-with-singularity`: direction of singularity we want to use
  - :bash:`-w`: direction where work will be generate
  - :bash:`-resume`: use the results already created in the work if the command has already been executed

For more details about rbx_flow use the command:

    .. code-block:: bash

        nextflow ${FLOW_DIR}/rbx_flow/main.nf --help

Or you can check the documentation for reconbundles `here <https://scil-documentation.readthedocs.io/en/latest/our_tools/recobundles.html>`_.

.. warning:: RBx_flow has no function for choosing the direction of the output, so in a second step we need to move our RBx_flow result in the RBx_flow_test direction.

    .. code-block:: bash

        mv results_rbx RBx_flow_test

References : 
    * St-Onge et al. (2023). BundleSeg: A versatile, reliable and reproducible approach to white matter bundle segmentation. `<https://arxiv.org/pdf/2308.10958.pdf>`_
    * Rheault, Francois. (2020). Analyse et reconstruction de faisceaux de la matière blanche. page 137-170. `<https://savoirs.usherbrooke.ca/handle/11143/17255>`_

Tractometry_flow
****************

#. Create the necessary direction for tractometry_flow inputs.

    .. code-block:: bash

        for i in tractometry_flow_test/raw/*; do mkdir ${i}/metrics ${i}/centroids ${i}/bundles; done

#. Import of data for tractometry_flow: diffusion metrics (fa, ad, md, rd) from tractoflow, centroids transformed and clean bundles from RBx_flow.

    .. code-block:: bash

        for i in tractoflow_test/results_tf/sub-*; do cp ${i}/DTI_Metrics/*__fa.nii.gz tractometry_flow_test/raw/$(basename $i)/metrics/; done
        for i in tractoflow_test/results_tf/sub-*; do cp ${i}/DTI_Metrics/*__ad.nii.gz tractometry_flow_test/raw/$(basename $i)/metrics/; done
        for i in tractoflow_test/results_tf/sub-*; do cp ${i}/DTI_Metrics/*__rd.nii.gz tractometry_flow_test/raw/$(basename $i)/metrics/; done
        for i in tractoflow_test/results_tf/sub-*; do cp ${i}/DTI_Metrics/*__md.nii.gz tractometry_flow_test/raw/$(basename $i)/metrics/; done

        for i in RBx_flow_test/results_rbx/sub-*; do cp ${i}/Transform_Centroids/*.trk tractometry_flow_test/raw/$(basename $i)/centroids/; done
        for i in tractometry_flow_test/raw/sub-*; do rm ${i}/centroids/*_Brainstem.trk; done

        for i in RBx_flow_test/results_rbx/*; do cp ${i}/Clean_Bundles/*.trk tractometry_flow_test/raw/$(basename $i)/bundles/; done
        for i in tractometry_flow_test/raw/sub-*; do rm ${i}/bundles/*_Brainstem_cleaned.trk; done

#. Run tractometry_flow.

    .. code-block:: bash

        nextflow ${FLOW_DIR}/tractometry_flow/main.nf --input tractometry_flow_test/raw --use_provided_centroids True \
         --output_dir tractometry_flow_test/results_tm -with-singularity ./containers_scilus_1.6.0.sif \
         -w tractometry_flow_test/work -resume

Parameters:
  - :bash:`--input`: direction of our data
  - :bash:`--use_provided_centroids`: Use the provided pre-computed centroids from rbx_flow rather than using automatic computation
  - :bash:`--output_dir`: direction where results will be generate
  - :bash:`-with-singularity`: direction of singularity we want to use
  - :bash:`-w`: direction where work will be generate
  - :bash:`-resume`: use the results already created in the work if the command has already been executed

For more details about tractometry_flow use the command:

    .. code-block:: bash

        nextflow ${FLOW_DIR}/tractometry_flow/main.nf --help

Or you can check the documentation for tractometry_flow `here <https://github.com/scilus/tractometry_flow>`_.

References :
    * Beaudoin et al. (2021). Modern Technology in Multi-Shell Diffusion MRI Reveals Diffuse White Matter Changes in Young Adults With Relapsing-Remitting Multiple Sclerosis. `<https://doi.org/10.3389/FNINS.2021.665017>`_
    * Cousineau et al. (2017). A test-retest study on Parkinson's PPMI dataset yields statistically significant white matter fascicles. `<https://doi.org/10.1016/j.nicl.2017.07.020>`_

Visualization
*************

Once you've run your different scripts, you'll get different files in your different results. The first thing to do is to check your DTI metric in `MI-Brain <https://scil-documentation.readthedocs.io/en/latest/intro_to/explore_software.html#mi-brain>`_.

The second thing you can do is view the mosaic of your different bundles: 

    .. code-block:: bash

        scil_visualize_bundles_mosaic.py RBx_flow_test/results_rbx/sub-PT001_ses-1_acq-1/Register_Anat/sub-PT001_ses-1_acq-1__native_anat.nii.gz \
        RBx_flow_test/results_rbx/sub-PT001_ses-1_acq-1/Clean_Bundles/*cleaned.trk mosaic.png

        feh mosaic.png

Finally, tractometry_flow directly generates plots of the various profilometries of your bundles with DTI metrics.
These are very basic, but give you an initial overview of the profile of your bundles. In addition, it also generates json files with all the tractometry_flow data.
You can check these files either with Excel, or in python with pandas or polars.