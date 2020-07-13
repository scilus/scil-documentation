.. _ref_QC:

QC  (Quality check)
===================

We have a QC pipeline which creates a summary of the quality of your data.

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

*How to share my work?*

If you have reached this point, congratulations! You have run tractoflow, which uses a significant amount of computation time, and you have verified your data, which required a significant amount of your time. It would be great to ensure that other lab members don't need to reproduces the same steps for the same data. If you believe your data should be shared to the rest of the lab:

    1. Please ask at least one other person to double-check your QC. You can share your html files on our slack channel #help_me_qc_my_data.

    2. Plase talk with Arnaud. He will tell you the best way to include your processed data either to BrainData or to Beluga.
