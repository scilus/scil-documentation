FSL / FreeSurfer
================

.. role:: bash(code)
   :language: bash

FSL and FreeSurfer are two set of tools developped respectively by FMRIB, Oxford, UK and by MGH, Harvard, Boston. The two teams have collaborated to make their tools compatible.

FSL
---

*What is it?*

    FSL is a set of tools to analyse FMRI, MRI and DTI brain imaging data. Here is the link to their `wiki page <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/>`_.

    In the lab, we mainly use `Bet <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/BET>`_ (for skullstripping).

    Previously, we also used some of these tools, but now we prefer FreeSurfer or Ants: `FAST <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FAST>`_ (to segment a T1 into GM, WM, CSF), `FIRST <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FIRST>`_ (for subcortical GM segmentation), and `FLIRT <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FLIRT>`_/`FNIRT <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FNIRT>`_ (for linear/non-linear registration).

*How to install it?*

    To install, you must download fslinstaller.py at https://fsl.fmrib.ox.ac.uk/fsldownloads_registration. You will have to create an account.

    Then from a terminal: :bash:`python fslinstaller.py`.

FreeSurfer
----------

*What is it?*

    Freesurfer offers similar tools. We use it for its cortex and subcortical parcellation based on atlases. You can find more information on their `main page <https://surfer.nmr.mgh.harvard.edu/>`_.

*How to install it?*

    If you plan to run freesurfer, note that we have a singularity and nextflow pipeline to run recon-all from Freesurfer 6. Moreover, if you plan to run freesurfer for multiple subjects, ask people in the lab how to do this on CBRAIN. It is the most efficient way to do so.

