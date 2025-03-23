
SET (Surface Enhanced Tractography)
===================================


.. role:: bash(code)
   :language: bash

1. Run Tractoflow (ref page)

2. Run civet or freesurfer:

    One possibility is to use CBrain. If you have access to that plateform, that's probably the easiest.

3. QC civet:

    CBrain

    What to expect

4. Download SET:

    1. The singularity (from ???), ex set_1v1.img

    2. The nextflow (https://github.com/StongeEtienne/set-nf)

5. Run SET:

    .. code-block:: bash

        nextflow run $SET/main.nf \
            -profile civet2_dkt \
            --tractoflow $tractoflow_output \
            --surfaces $civet_output \
            -with-report report_basic.html \
            --output_dir $set_output \
            -with-singularity $singularity \
            -resume --processes 4

    ** Please note that if you used a recent version of tractoflow, you might need to change line 155 in the main script (https://github.com/StongeEtienne/set-nf/blob/main/main.nf) because PFT_Maps is sometimes called PFT_Tracking_Maps in newer versions.

6. QC results:

    Check the vtk file D_SurfaceFlow/*_100_1.0.vtk (MI-brain, ref, can load this vtk file). It shows the first steps of your streamlines.