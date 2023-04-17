Intro to Software
=======================

.. role:: bash(code)
   :language: bash


\section{Intro to Software}


MI-Brain
"""""""""""""""""""""""
MI-Brain is a Diffusion MRI and Tractography visualization software designed to help medical professionals and researchers look and explore their data. It provides many features and tools for processing and visualizing tractograms.

Make sure to download the software from Github `(here) <https://github.com/imeka/mi-brain/releases>`__ and read the wiki and watch the videos (linked below). If you are heavily using MI-Brain in your research, please cite:

    *Rheault, F., Houde, J-C., Goyette, N., Morency, F., Descoteaux, M., MI-Brain, a software to handle tractograms and perform interactive virtual dissection, ISMRM Diffusion study group workshop, Lisbon, 2016.*

.. figure:: /images/intro_to_software_mi_brain.png
    :scale: 25 %
    :align: center

    MI-Brain facilitate bundle segmentation and basics image/mask operations.

Related links
    - MI-Brain cheatsheet `[link] <https://github.com/imeka/mi-brain/wiki/>`__
    - Video tutorial `[link] <https://www.youtube.com/playlist?list=PLfVC14bBRTsVHzuWqfzrPp3MtYfPETDgu>`__
    - Conference abstract `[link] <https://www.researchgate.net/publication/312190253_MI-Brain_a_software_to_handle_tractograms_and_perform_interactive_virtual_dissection>`__

FSL
"""""""""""""""""""""""
FSL (FMRIB Software Library) is an open-source software library for neuroimaging analysis. It provides a comprehensive suite of tools for processing, analyzing, and visualizing neuroimaging data (Structural, Functional and Diffusion MRI). It is widely used in academic and clinical research.

Visit this website for download and install instructions as well as a general overview of tools available in the package `(here) <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki>`__

You will have to download a Python file install (after accepting a license) and then install FSL (by executing the Python installer)
`(here) <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation>`__

It is common to add these lines to your :bash:`.bashrc` to make FSL easier to use;

.. code-block:: bash

    # export FSLDIR=/PATH/TO/FSL
    . ${FSLDIR}/etc/fslconf/fsl.sh
    export PATH=${FSLDIR}/bin:${PATH}

Once installed, you should be able to type :bash:`bet` or :bash:`fast` to see the help display. :bash:`fsleyes` will launch the visualization tool.


.. figure:: /images/intro_to_software_fsl.png
    :scale: 40 %
    :align: center

    FSLeyes used here to visualize fMRI data.


Functional MRI
^^^^^^^^^^^^^^^^^^^^^

:bash:`feat` is a user-friendly FMRI analysis tool that includes data preprocessing, timeseries analysis, and group analysis using Bayesian techniques.

:bash:`melodic` is an FMRI analysis tool that uses Probabilistic Independent Component Analysis (PICA) to automatically estimate the number of signal and noise sources in the data and provide "p-values" for the output spatial maps.

Structural MRI
^^^^^^^^^^^^^^^^^^^^^

:bash:`bet` is the Brain Extraction Tool, which segments the brain from non-brain in structural and functional data and models skull and scalp surfaces.

:bash:`fast` is FMRIB's Automated Segmentation Tool, which provides brain segmentation (into different tissue types) and bias field correction.

:bash:`flirt` is FMRIB's Linear Image Registration Tool, which offers linear inter- and intra-modal registration.

:bash:`fnirt` is FMRIB's NonLinear Image Registration Tool, which offers linear inter- and intra-modal registration.

:bash:`siena` is a structural brain change analysis tool used for estimating brain atrophy.

:bash:`susan` is a nonlinear noise reduction tool.

Diffusion MRI
^^^^^^^^^^^^^^^^^^^^^
:bash:`bedpostx` is a tool in FSL that uses Bayesian estimation with Markov Chain Monte Carlo sampling to model diffusion MRI signal as fiber orientation distributions and estimate diffusion parameters at each voxel for local modeling of diffusion parameters, including estimation of the number and orientation of fiber bundles.

:bash:`probtrackx` is a tool in FSL that performs tractography and connectivity-based segmentation using probabilistic tractography. It calculates the probability of connection between pairs of voxels in the brain by simulating diffusion-weighted MRI signal propagation along different possible fiber pathways to investigate the connectivity of different brain regions and segment the brain into functional networks based on connectivity patterns.

:bash:`eddy` is a tool that performs eddy current correction and motion correction for diffusion MRI data.

:bash:`topup` is a tool that corrects for susceptibility-induced distortions in diffusion MRI data.

:bash:`xtract` (cross-species tractography) is a tool that automatically extract a set of tracts in humans and macaques. It can also be used to define one's own tractography protocols where all the user needs to do is to define a set of masks in standard space (e.g. MNI152).

TBSS is Tract-Based Spatial Statistics, part of FMRIB's Diffusion Toolbox, which offers voxelwise analysis of multi-subject diffusion data.


ANTs
"""""""""""""""""""""""
ANTs (Advanced Normalization Tools) is a powerful open-source software package for (medical) image analysis registration and segmentation. Extremely useful to create templates or extract cortical thickness. It is widely used in the field of neuroimaging.

Visit this website for download and install instructions \href{https://github.com/ANTsX/ANTs/wiki/Compiling-ANTs-on-Linux-and-Mac-OS}{\color{blue}{[link]}}. as well as a general overview of tools available in the package \href{https://github.com/ANTsX/ANTs}{\color{blue}{[link]}}. ANTs use a pretty complex algorithm, so the command line is sometimes hard to understand at first, this should help \href{https://github.com/ANTsX/ANTs/wiki/Anatomy-of-an-antsRegistration-call}{\color{blue}{[link]}}.

Once installed, you should be able to type \verb|antsRegistration| or \verb|antsApplyTransforms| to see the help display.

MRtrix
"""""""""""""""""""""""
MRtrix is an open-source software package for diffusion MRI analysis and Tractography. It provides a suite of tools for processing, analyzing, and visualizing diffusion MRI data and streamlines. It is widely used in research and clinical applications.
Visit this website for download and install instructions as well as a general overview of tools available in the package \href{https://www.mrtrix.org/}{\color{blue}{[link]}} (click Documentation).

This webpage hosts an extensive tutorial of mrtrix3 from raw data to tractography (and more) \href{https://osf.io/fkyht/}{\color{blue}{[link]}}. We recommend trying this tutorial and finding analogous functions in Scilpy to reach the same end goals.

Once installed, you should be able to type \verb|dwi2fod| or \verb|mrview| to see the help display.

MRIcroGL
"""""""""""""""""""""""
MRIcroGL is an open-source software package for the visualization of MRI data. It provides tools for visualizing MRI data in 2D and 3D. There are a lot of options for shaders, volume rendering, and automatic screenshots for research projects.

Visit this website for download and install instructions \href{https://github.com/rordenlab/MRIcroGL}{\color{blue}{[link]}} as well as a general overview of tools available in the package \href{https://www.nitrc.org/plugins/mwiki/index.php/mricrogl:MainPage}{\color{blue}{[link]}}.

Once installed, you should be able to type \verb|dcm2niix| or \verb|MRIcroGL| to see the help display.


Freesurfer
"""""""""""""""""""""""
Freesurfer is an open-source software package for brain surface reconstruction and analysis. It provides a suite of tools for processing, analyzing, and visualizing brain surface data. It is widely used in research and clinical applications, it is often the tool of choice to generate cortical and/or subcortical parcellations.

Visit this website for download and install instructions \href{https://surfer.nmr.mgh.harvard.edu/fswiki}{\color{blue}{[link]}}. as well as a general overview of tools available in the package.

Once installed, you should be able to type \verb|recon-all| or \verb|mri_convert| to see the help display.
