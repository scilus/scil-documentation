.. _ref_fsl_freesurfer:

FSL / FreeSurfer / FastSurfer
=============================

.. role:: bash(code)
   :language: bash

FSL and FreeSurfer/FastSurfer are two set of tools developed respectively by FMRIB, Oxford, UK and by MGH, Harvard, Boston. The two teams have collaborated to make their tools compatible.

FSL
---

*What is it?*

    FSL is a set of tools to analyse FMRI, MRI and DTI brain imaging data. Here is the link to their `wiki page <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/>`_.

    In the lab, we mainly use `Bet <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/BET>`_ (for skullstripping) and `FAST <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FAST>`_ (to segment a T1 into GM, WM, CSF)

    Previously, we also used some of these tools, but now we prefer FreeSurfer or Ants: `FIRST <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FIRST>`_ (for subcortical GM segmentation), and `FLIRT <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FLIRT>`_/`FNIRT <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FNIRT>`_ (for linear/non-linear registration).

*How to install it?*

    To install, you must download fslinstaller.py at https://fsl.fmrib.ox.ac.uk/fsldownloads_registration. You will have to create an account.

    Then from a terminal: :bash:`python fslinstaller.py`. (Note that this only works on python2.7. See the Environments section for help on how to use a different python version).

FreeSurfer
----------

*What is it?*

    `Freesurfer <https://surfer.nmr.mgh.harvard.edu/>`_ offers similar tools. We use it for its cortex and subcortical parcellation based on atlases. Note that a similar project is :ref:`ref_civet`

*How to install it?*

    If you plan to run freesurfer, note that we have a singularity and nextflow pipeline to run recon-all from Freesurfer 6. Moreover, if you plan to run freesurfer for multiple subjects, ask people in the lab how to do this on CBRAIN. It is the most efficient way to do so.

    Else, you can run some commands (e.g. recon-all) through cbrain, see the :ref:`ref_cbrain` tab for more information. When you launch it, remember to select option "multiple" if the files come from multiple subjects.

FastSurfer
----------

*What is it?*

    `FastSurfer <https://deep-mi.org/research/fastsurfer/>`_ is an alternative to FreeSurfer based on machine learning (a CNN). The process is greatly accelerated (in terms of minutes instead of hours).