.. _ref_scilpy_page:

SCILPY / DIPY
==============

DIPY
####

*What is it?*

    Dipy is a diffusion MRI data analysis. It is similar to MRtrix (see the "Other tools" section). One of Dipy's main authors and contributors, Eleftherios Garyfallidis, was a post-doc in our lab in 2014-2015. It offers many functions coded in python/cython that you can import as a library when analysing your data. It doesn't offer complete end-to-end scripts, but you can check their `official website <https://dipy.org/>`_'s tutorials for scripts examples.

*How to install it?*

    You can find instructions on their `github page <https://github.com/nipy/dipy>`_. But note that if you install Scilpy (see lower), it will install Dipy at the same time.


SCILPY
######

*What is it?*

    Scilpy is closely related to Dipy: it follows the same organization. But it also contains work that has been developped by our lab and that is not included yet into Dipy. We have a `public version <https://github.com/scilus/scilpy>`_ of Scilpy on Github, with work that has been tested and that we want to share with the community, and a private version on Bitbucket (you have to ask for access) with our work that is either not tested, still being developped or not converted into python 3.

    Scilpy contains two main folders: the scilpy folder with the Dipy-like library, and the scripts folder with a list of python scripts ready to be called from the terminal in command line. For each script, you can use the -h option for explanations on how to use it. Ex:

    .. code-block:: bash

        scil_compute_fodf.py -h

*How to install it*

    Users: you can follow the instructions on the Github page. Clone the repository, install the requirements and install through the setup.py as explained.

Our nextflows
##############

*What is it?*

If you want to run many scripts, on many subjects, one way would be to prepare a bash script (.sh) to run your study. Ex:

    .. code-block:: bash

        subjects="S01 S02 etc."
        for subj in $subjects
        do
            inputs=PATH_TO_INPUT
            bvals=PATH_TO_BVALS
            bvecs=PATH_TO_BVECTS
            frf_file=PATH_TO_FRF
            out_name=OUTPUT_NAME
            # etc.

            scil_compute_somestep
            ...
            scil_compute_fodf.py --fodf $out_name $input $bvals $bvecs $frf_file
            scil_compute_someotherstep
            ...
        done

    But analysing data often requires many steps. Preparing your own bash script with all those steps, with all the right options, could be fastidious. Our lab has prepared pipelines as nextflows (see the 'Nexflow' section in 'Other tools') that you can use to analyse all your data in only one simple script, such as the `Tractoflow <https://tractoflow-documentation.readthedocs.io/en/latest/pipeline/steps.html>`_, which does all the preprocessing on DWI data and T1 data and performs the wholebrain tracking.

    Once the preprocessing and the tracking are done, scilpy also contains scripts to separate your data into know bundles (Recobundles), vizualize your results (ex, scil_visualize_bundles_mosaic.py), create statistics on your bundles and so on. We have a QA pipeline which creates a summary of the quality of your data, you can ask Guillaume if you are interested. You can also ask François for his tractometry repo.

    Please also see the 'Dealing with heavy data' section to learn on super computers. Processing data could be very long on your computer, but we have lab access to computing platforms.

*How to install it*

You can check the `installation guide <https://tractoflow-documentation.readthedocs.io/en/latest/installation/before_install.html>`_ on Tractoflow's website.