.. _ref_other_pipelines:

After tractoflow
================

.. role:: bash(code)
   :language: bash

Once the preprocessing and the tracking are done, scilpy also contains scripts to separate your data into known bundles (Recobundles), visualize your results (ex, scil_visualize_bundles_mosaic.py), compute statistics on your bundles and so on.

QA/ QC  (Quality assurance, Quality check)
------------------------------------------

We have a QC pipeline which creates a summary of the quality of your data. For now it is in Guillaume's repository but is should be added to the SCIL's Github soon.

*How to install it?*

    To install it, you may clone its nextflow version:


    .. code-block:: bash

        pip install git+https://github.com/GuillaumeTh/dmriqcpy.git
        git clone https://github.com/GuillaumeTh/dmriqc-flow.git

    And then to download the latest singularity image: go on this page: https://github.com/GuillaumeTh/dmriqcpy/actions, click on the latest event, then click on the singularity under "Artifacts". The download should start.

*How to use it?*

    .. code-block:: bash

        tractoflow_results=YOUR_PATH
        path_QC_flow=WHERE_YOU_CLONED_IT
        singularity_name=qa.img

        mkdir $results_path/QA
        cd  $results_path/QA

        nextflow run $path_QA/main.nf --root $results_path -with-singularity $singularity_name



RecobundlesX
------------

ToDO

BundleReporting
---------------

ToDo

Tractometry
-----------

ToDo