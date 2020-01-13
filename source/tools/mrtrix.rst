MRtrix
======

.. role:: bash(code)
   :language: bash

*What is it?*

    MRtrix is another set of tools to analyse diffusion data, much like Dipy and scilpy. One main difference is that they use C++ whereas we use python. Here are the links to their `website <https://www.mrtrix.org/>`_ and their `documentation <http://userdocs.mrtrix.org/en/latest/index.html>`_.

    In the lab, we use some of their tools for which Dipy/scilpy don't have strong equivalents, such as `mrconvert <https://mrtrix.readthedocs.io/en/latest/reference/commands/mrconvert.html>`_ (ex, to convert MRI data from DICOM files to Nifti files), `mrview <https://mrtrix.readthedocs.io/en/latest/reference/commands/mrview.html>`_, their GUI to view images, mrinfo to retrieve information on a dataset from its header, or other such scripts.

    MRtrix pipeline is very similar in spirit to the Scilpy/DIPY and Tractoflow pipeline we implement at the SCIL. Both tools were created more or less at the same time. Both are open source.

    The common parts are the pre-processing tools calling some FSL/ANTS, the constrained spherical deconvolution to produce the fODF and novel HARDI fixel-based metrics (NuFO, AFD), the anatomical constrainted tractography (ACT) and deterministic/probabilistic streamline-based tracking, which ressembles our local tracking strategy and particle filter tractography with anatomical priors.

    MRtrix's avantages: MRtrix is generally faster than Scilpy/DIPY. Generally, MRtrix's strong suit concerns the connectomics, voxel information (ex: nb of streamlines in a voxel). MRtrix also added their fixel-based analysis, which is like a VBM or TBSS in the space of fODF fixels (i.e. voxels, but per fiber population). See [`Raffelt et al 2015 <https://doi.org/10.1016/j.neuroimage.2015.05.039>`_, `Mito et al 2018 <https://doi.org/10.1093/brain/awx355>`_]. \*MRtrix also has a multi-shell CSD implementation that we should soon have in Scilpy/DIPY, to support fODF reconstruction from multi-b-value DWI.

    Scilpy/DIPY's advantages: Scilpy/DIPY is written in python, which might be easier to read by the community than MRtrix's C++. Its strong suit concerns the fibers and the bundles instead of the voxels, with tools such as Recobundles, outlier rejection, tractometry and so on.

*How to install it?*

    In a terminal, from the directory where you want to install it:

    .. code-block:: bash

        git clone https://github.com/MRtrix3/mrtrix3.git
        cd mrtrix3
        ./configure
        NUMBER_OF_PROCESSORS=8  # If you want to set the number of threads your computer should use.
        ./build

    Then you could add these lines in your .bashrc:

    - From a terminal: :bash:`sudo gedit ~/.bashrc`
    - Copy this in your file:

        .. code-block:: bash

            export PATH=~/Code/mrtrix3/bin:${PATH}



