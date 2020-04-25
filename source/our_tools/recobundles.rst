RecobundlesX
============

Here is a typical example of a script to run our scilpy's version of Recobundles on a batch of subjects. Dipy also has its version, and you can find the explanation `here <https://dipy.org/documentation/0.16.0./examples_built/bundle_extraction/>`_.

In the following script, we take the example of data that has been preprocessed using :ref:`ref_tractoflow`. tractoflow_folder is your root, which should contain tractoflow's results for each subject. This script will create a Recobundles folder inside each subject's directory.

You will need :ref:`ref_ants`

.. code-block:: bash

    tractoflow_folder=my_dir
    subject_list=my_subject_list.txt
    models_path=YOUR_PATH         # Ex: hcp_models/
    model_T1=THE_T1               # Ex: $models_path/mni_masked.nii.gz
    model_config=JSON_FILE        # Ex: $models_path/config_python.json
    model_streamlines_files=FILES # Ex: $models_path/*/. Files like AF_L.trk, AF_R.trk, etc.

    # Filtering options. Change as needed.
    minL=20
    maxL=200

    # RecobundlesX options. Change as needed.
    nb_total_executions=9    # Nb bundles * nb_per_bundle (see json) = max total executions
    thresh_dist="10 12"
    processes=6              # Number of thread used for computation
    seed=0                   # Random generator.
    minimal_vote=0.5         # Saving streamlines if recognized often enough


    while IFS= read -r subj; do
        echo "Running subject $subj"

        # Defining subj folders
        subj_folder=$tractoflow_folder/$subj
        rbx_folder=$subj_folder/RecobundlesX
        if [ ! -d "$rbx_folder" ]; then
          mkdir "$rbx_folder"
        else
          echo "The RecobundlesX folder already exists!!! Please delete it first."
          echo "($rbx_folder)"
          exit 1
        fi

        # Defining inputs
        subj_trk=$subj_folder/Tracking/${subj}__tracking.trk
        subj_T1=$subj_folder/Register_T1/${subj}__t1_warped.nii.gz

        ###
        # Registering model on subject (using ANTS)
        #   d=image dimension,
        #   f=fixed image, m=moving image
        #   -t: transformation a = rigid+affine
        #   n = nb of threads
        # This should create 3 files : model_to_subj_anat0GenericAffine.mat,
        # model_to_subj_anatInverseWarped.nii.gz and  model_to_subj_anatWarped.nii.gz
        ###
        model_on_subj=$rbx_folder/model_to_subj_anat
        antsRegistrationSyNQuick.sh -d 3 -f $subj_T1 -m $model_T1 -t a -n 4 -o $model_on_subj

        ###
        # Generating affine txt file (using ANTS)
        ###
        affine=${model_on_subj}0GenericAffine.txt
        ConvertTransformFile 3 ${model_on_subj}0GenericAffine.mat $affine --hm --ras

        ###
        # Cleaning tracking file to make sure it is not too big.
        # Recobundles is already long enough :) .
        ###
        subj_filtered_trk=$subj_folder/Tracking/${subj}__tracking_filteredLength.trk
        scil_filter_streamlines_by_length.py --minL $minL --maxL $maxL $subj_trk $subj_filtered_trk

        ###
        # Scil's Recobundle
        #   processes = nb of threads.
        #   Seed = rnd generator seed.
        #   inverse is to use the inverse affine
        ###
        mkdir $rbx_folder/multi_bundles
        scil_recognize_multi_bundles.py --output $rbx_folder/multi_bundles \
            --multi_parameters $nb_total_executions --tractogram_clustering_thr $thresh_dist  \
            --processes $processes --seeds $seed --inverse -f --log_level DEBUG \
            --minimal_vote_ratio $minimal_vote \
            $subj_filtered_trk $model_config $model_streamlines_files $affine

    done < $subject_list

To visualize your results for one subject, here is a nice tool:

    .. code-block:: bash

        # Run from inside your RecobundlesX folder
        anat=YOUR_ANAT
        scil_visualize_bundles_mosaic.py $anat *.trk mosaic.png

Here is a nice example to help your compare your results. This was created from a HCP subject.


.. image:: ../images/mosaic_part1.png
    :scale: 50 %
    :align: center

.. image:: ../images/mosaic_part2.png
    :scale: 50 %
    :align: center