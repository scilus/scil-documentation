RecobundlesX
============

Here is a typical example of a script to run our scilpy's version of Recobundles on a batch of subjects. Dipy also has its version, and you can find the explanation `here <https://dipy.org/documentation/0.16.0./examples_built/bundle_extraction/>`_.

In the following script, we take the example of data that has been preprocessed using :ref:`ref_tractoflow`. tractoflow_folder is your root, which should contain tractoflow's results for each subject. This script will create a Recobundles folder inside each subject's directory.

You will need :ref:`ref_ants`

.. code-block:: bash

    tractoflow_folder=my_dir
    subject_list=my_subject_list.txt
    model_T1=my_model.nii.gz  # Ex: hcp_models/mni_masked.nii.gz

    # Filtering options. Change as needed.
    minL=20
    maxL=200

    # Recobundles options. Change as needed.
    nb_total_tests=9    # Nb bundles * nb_per_bundle (see json) = max total tests
    thresh_dist_qb_myStreamlines="10 12"
    processes=6         # Number of thread used for computation
    seed=0              # Random generator.
    minimal_vote=0.5    # Saving streamlines if recognized often enough


    while IFS= read -r subj; do
        echo "Running subject $subj"

        # Defining subj folders
        subj_folder=$tractoflow_folder/$subj
        rbx_folder=$subj_folder/Recobundles
        if [ ! -d "$rbx_folder" ]; then
          mkdir "$rbx_folder"
        else
          echo "The Recobundles folder already exists!!! Please delete it first."
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
        ###
        model_on_subj=$rbx_folder/model_to_subj_anat
        antsRegistrationSyNQuick.sh -d 3 -f $subj_T1 -m $model_T1 -t a -n 4 -o $model_on_subj

        ###
        # Generating affine
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
        scil_recognize_multi_bundles.py $subj_filtered_trk $model_config $model_streamlines_files $affine \
            --output_dir $output_dir/multi  --multi_parameters $nb_total_tests \
            --tractogram_clustering $thresh_dist_qb_myStreamlines \
            --processes $processes --seeds $seed --inverse -f --log_level DEBUG --minimal_vote $minimal_vote

    done < $subject_list