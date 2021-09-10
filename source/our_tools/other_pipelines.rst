.. _ref_other_pipelines:

Checks and stats
================

.. role:: bash(code)
   :language: bash

Once the preprocessing and the tracking are done, scilpy also contains scripts to separate your data into known bundles (Recobundles), vizualize your results (ex, scil_visualize_bundles_mosaic.py), compute statistics on your bundles and so on.


QA/ QC  (Quality assurance, Quality check) -- tractoflow
--------------------------------------------------------

We have a QC pipeline which creates a summary of the quality of your tractoflow results.

*How to install it?*

    The easiest is to use it as a nextflow with singularity (see :ref:`ref_nextflow` for more information.) First download the singularity image (.img) here: https://github.com/GuillaumeTh/dmriqcpy/releases. Then, download the nextflow:

    .. code-block:: bash

        git clone https://github.com/GuillaumeTh/dmriqc-flow.git

*How to run it?*

    .. code-block:: bash

        nextflow run PATH_TO_DMRIQC_FLOW/main.nf --root TRACTOFLOW_RESULTS -with-singularity PATH_TO_THE_DMRIQC_SINGULARITY -resume

*How to use it?*

This produces a QC report for each important section of the tractoflow. For instance, you may check the quality of the registration step, or compare the FA of all your subjects. You can check each html file by double-clicking on it in your file explorer. Check the interrogation mark on the top right corner for a list of shortcuts. The QC typically raises warning when a subject is very different from the others. You can then check each tab, each subject for a visual inspection. Scroll through the subjects with the arrows. For each subject, you can then decide if the quality level was acceptable (hit 1,2 or 3 for pass, warning or fail), and leave comments in the comment box.

We will soon add here a list of characteristic you should expect to see for each metric, to help beginners develop an expert eye when looking at processed data.


QA/ QC  (Quality assurance, Quality check) -- recobundlesX
----------------------------------------------------------

To assess the quality of your bundles, the best way is to check the data visually using the mosaic, as described on the RecobundlesX page. However if you possess the ground truth for your data, you may use tractometry for your statistics.


Tractometry
-----------

If you have a ground truth, you can compute statistics for each bundle using the metrics that were introduced in the tractometer. You can find the definition of each metric (ex., VB, IB, VC, IC, OL, OR) on the `tractometer website <http://tractometer.org/ismrm_2015_challenge/evaluation>`_. To compute them, you can use scilpy's script `scil_evaluate_bundles_pairwise_agreement_measures.py`.


Sharing your work
-----------------

If you have reached this point, congratulations! You have run processes that use a significant amount of computation time, and you have verified your data, which required a significant amount of your time. It would be great to ensure that other lab members don't need to reproduces the same steps for the same data. If you believe your data should be shared to the rest of the lab:

    1. Please ask at least one other person to double-check your QC. You can share your html files on our slack channel #HelpMeQcMyData.

    2. Please talk with Arnaud. He will tell you the best way to include your processed data either to BrainData or to Beluga.
