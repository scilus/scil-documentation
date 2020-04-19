.. _ref_other_pipelines:

After tractoflow
================

.. role:: bash(code)
   :language: bash

Once the preprocessing and the tracking are done, scilpy also contains scripts to separate your data into known bundles (Recobundles), vizualize your results (ex, scil_visualize_bundles_mosaic.py), compute statistics on your bundles and so on.

QA/ QC  (Quality assurance, Quality check)
------------------------------------------

We have a QC pipeline which creates a summary of the quality of your data.

*How to install it?*

    The easiest is to use it as a nextflow with singularity (see :ref:`ref_nextflow` for more information.) First download the singularity image: On this page, https://github.com/GuillaumeTh/dmriqcpy/actions, click on the latest version, then under "Artifacts", click on the singularity to start the download. You should take a note somewhere to remember which version you downloaded. Then, download the nextflow:

    .. code-block:: bash

        git clone https://github.com/GuillaumeTh/dmriqc-flow.git

*How to use it?*

    .. code-block:: bash

        tractoflow_results=YOUR_PATH
        path_QC_nextflow=WHERE_YOU_CLONED_dmriqc-flow
        singularity_img=WHERE_YOU_DOWNLOADED/singularity_dmriqc_*.img

        nextflow run $path_QC_nextflow/main.nf --root $tractoflow_results -with-singularity $singularity_img -resume

RecobundlesX
------------

ToDO

BundleReporting
---------------

ToDo

Tractometry
-----------

ToDo